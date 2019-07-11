
### GROUP BY
- select, from, where 절 다음에 기술한다.
- 특정 컬럼(들)의 값별로 나눠 집계할 때 나누는 기준컬럼을 지정하는 구문.

ex) emp 테이블

| 부서 | 직원 | 급여 |  
|:---:|:---:|:---:|
|  IT  |  A  | 100 | 
|  IT  |  B  | 200 |
|  DB  |  C  | 300 |
|  DB  |  D  | 400 |
|  DB  |  E  | 500 |

문제) 부서별로 급여의 합계를 조회  

```sql
select distinct dept_name 부서 from emp -- (1)
select sum(salary) 부서 from emp; -- (2)
select distinct dept_name 부서, sum(salary) 급여합계 from emp; -- (3)
```

(1)번 퀴리의 결과

| 부서 |
|:----:|
|  IT  |
|  DB  |

(2)번 쿼리의 결과

| 급여합계 |
|:---:|
| 1500 |

(3)번 쿼리의 결과 --> 에러  
 > dept_name의 결과는 IT부서와 DB부서로 2행인 다중행이 나온다.  
그런데 sum(salary)를 하면 IT부서만의 급여 합계와 DB부서만의 급여 합계가 나오지 않고,  
IT부서와 DB부서의 급여를 모두 합한 하나의 결과인 1행, 즉 단일행이 나온다.  
(집계함수의 결과는 항상 단일행이다.)

=> 전체가 아닌 부서별로 따로 묶어서 급여를 구해야 한다.

```sql
select dept_name 부서, sum(salary) 급여합계 from emp group by dept_name;
```

결과)

| 부서 | 급여합계 |
|:----:|:----:|
|  IT  | 300 |
|  DB  | 1200 |

- group by 컬럼 : 컬럼에서 동일한 값끼리 그룹으로 묶는다.  
=> 집계함수를 사용 할 경우, 그룹별로 집계를 진행한다.

****

| 회사 | 부서 | 직원 | 급여 |  
|:----:|:---:|:---:|:---:|
|  KT  |  IT  |  A  | 100 | 
|  KT  |  IT  |  B  | 200 |
|  KT  |  DB  |  C  | 300 |
|  KT  |  DB  |  D  | 400 |
|  KT  |  DB  |  E  | 500 |
|  SK  |  IT  |  F  | 100 | 
|  SK  |  IT  |  G  | 200 |
|  SK  |  IT  |  H  | 300 |
|  SK  |  DB  |  I  | 400 |
|  SK  |  DB  |  J  | 500 |

```sql
select company 회사, dept_name 부서, sum(salary) 급여합계 from emp group by company, dept_name;
```

결과)

| 회사 | 부서 | 급여 |
|:----:|:----:|:----:|
|  KT  |  IT  | 300 |
|  KT  |  DB  | 1200 |
|  SK  |  IT  | 600 |
|  SK  |  DB  | 900 |

- group by 컬럼1, 컬럼2, ...  
: 컬럼1에서 동일한 값끼리 그룹으로 묶고, 해당 그룸 안에서 컬럼2에서 동일한 값끼리 그룹으로 묶고, ...

****

- 부서별(dept_name) 직원수를 조회

```sql
select dept_name 부서, count(*) 직원수 from emp group by dept_name;
```

###### 결과

![결과11-1](/image_file/결과11-1.png)

- 업무별(job) 직원수를 조회 (직원수가 많은 것부터 정렬)

```sql
select job 업무, count(*) 직원수 from emp group by job order by 2 desc;
```

###### 결과

![결과11-2](/image_file/결과11-2.png)

- 부서명(dept_name), 업무(job)별 직원수, 최고급여(salary)를 조회 (부서이름으로 오름차순 정렬)

```sql
select dept_name 부서, job 업무, count(*) 직원수, max(salary) 최고급여
from emp
group by dept_name, job
order by 1;
```

###### 결과

![결과11-3](/image_file/결과11-3.png)

- EMP 테이블에서 입사연도별(hire_date) 총 급여(salary)의 합계을 조회  
(급여 합계는 자리구분자 , 를 넣으시오. ex: 2,000,000)

```sql
select to_char(hire_date, 'yyyy') 입사연도, to_char(sum(salary), '9,999,999') "총 급여"
from emp
group by to_char(hire_date, 'yyyy');
```

###### 결과

![결과11-4](/image_file/결과11-4.png)

- 급여(salary) 범위별 직원수를 조회 (급여 범위는 10000 미만,  10000이상 두 범주)

```sql
select case when salary < 10000 then '10000 미만'
            else '10000 이상' end as 급여범위,
       count(*) 직원수
from emp 
group by case when salary < 10000 then '10000 미만'
              else '10000 이상' end;
```

###### 결과

![결과11-5](/image_file/결과11-5.png)

- 급여 범위별 직원수를 조회 (급여 범위는 5000 미만, 5000이상 10000 미만, 10000이상 20000미만, 20000이상)

```sql
select case when salary < 5000 then '5000미만'
            when salary between 5000 and 9999 then '5000이상 10000미만'
            when salary between 10000 and 19999 then '10000이상 20000미만'
            else '2000이상'
            end as "급여 범위", 
            count(*) 직원수
from emp
group by case when salary < 5000 then '5000미만'
              when salary between 5000 and 9999 then '5000이상 10000미만'
              when salary between 10000 and 19999 then '10000이상 20000미만'
              else '2000이상'
              end
order by decode("급여 범위", '5000미만', 1, '5000이상 10000미만', 2, '10000이상 20000미만', 3, 4);
```

###### 결과

![결과11-6](/image_file/결과11-6.png)

****


