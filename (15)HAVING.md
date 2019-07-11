
### HAVING
- 집계 결과에 대한 행 제약 조건  
- 제약조건의 연산자는 where절의 연산자를 사용
- select, from, where, group by 다음에, order by 전에 온다.

****

### 데이터의 조회 순서 (select, from , where, group by, having, order by)  
1. from - 어느 테이블에서 데이터를 조회할지 선택  
2. where - 조회하려는 테이블에서 조건에 맞지 않는 데이터를 걸러낸다.  
3. group by - where 조건으로 걸러진 데이터를 가지고, 기준컬럼으로 그룹을 묶는다.  
4. having - group by로 나온 결과에서 having의 조건에 맞지 않는 결과를 걸러낸다.  
5. select - having으로 나온 결과에서 필요한 컬럼만 뽑아낸다.  
6. order by - select로 나온 결과를 기준컬럼의 데이터로 정렬한다.  
7. 결과 출력  

****

- 직원수가 10 이상인 부서의 부서명(dept_name)과 직원수를 조회

```sql
select dept_name 부서명, count(*) 직원수
from emp
group by dept_name
having count(*) >= 10;
```

###### 결과

![결과12-1](/image_file/결과12-1)

- 15명 이상이 입사한 년도와 (그 해에) 입사한 직원수를 조회

```sql
select to_char(hire_date, 'yyyy') 입사년도, count(*) 직원수
from emp
group by to_char(hire_date, 'yyyy')
having count(*) >= 15;
```

###### 결과

![결과12-2](/image_file/결과12-2)

- 평균 급여가(salary) $5000이상인 부서의 이름(dept_name)과 평균 급여(salary), 직원수를 조회

```sql
select dept_name, round(avg(salary), 2) 평균급여, count(*) 직원수
from emp
group by dept_name
having avg(salary) >= 5000;
```

###### 결과

![결과12-3](/image_file/결과12-3)

- 평균급여가 $5,000 이상이고 총급여가 $50,000 이상인 부서의 부서명(dept_name), 평균급여와 총급여를 조회

```sql
select dept_name, ceil(avg(salary)) 평균급여, sum(salary) 총급여
from emp
group by dept_name
having avg(salary) >= 5000 and sum(salary) >= 50000;
```

###### 결과

![결과12-4](/image_file/결과12-4)

****

