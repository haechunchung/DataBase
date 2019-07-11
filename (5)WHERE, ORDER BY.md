

### SELECT 컬럼 FROM 테이블명 WHERE 조건  
1. 숫자, 문자열,날짜 모두 >, >=, <, <=, =, != 비교

- EMP 테이블에서 직원_ID(emp_id)가 110인 직원의 이름(emp_name)과 부서명(dept_name)을 조회

```sql
select emp_name 직원이름, dept_name 부서명 from EMP where emp_id = 110;

```

###### 결과

![결과2-1](/image_file/결과2-1.png)

- EMP 테이블에서 'IT' 부서에 속하는 직원들의 ID(emp_id), 이름(emp_name), 부서명(dept_name)을 조회

```sql
select emp_id 직원ID, emp_name 이름, dept_name 부서명 from EMP where dept_name = 'IT';
```

###### 결과

![결과2-2](/image_file/결과2-2.png)

****

2. where 컬럼 between A and B : A <= 컬럼 <= B 을 만족시키는 데이터를 조회  
where 컬럼 not between A and B : 컬럼 > A 또는 B < 컬럼 을 만족시키는 데이터를 조회

- 급여(salary)가 $4,000에서 $8,000 사이에 포함된 직원들의 ID(emp_id), 이름(emp_name)과 급여(salary)를 조회

```sql
select emp_id 직원ID, emp_name 이름, salary 급여 from emp where salary between 4000 AND 8000;
```

###### 결과

![결과2-3](/image_file/결과2-3.png)

- 급여(salary)가 $4,000에서 $8,000 사이에 포함되지 않는 모든 직원들의  ID(emp_id), 이름(emp_name), 급여(salary)를 조회

```sql
select emp_id 직원ID, emp_name 이름, salary 급여 from emp where salary not between 4000 AND 8000;
```

###### 결과

![결과2-4](/image_file/결과2-4.png)

****

3. where 칼럼 in (A, B, C, ...) : 칼럼의 값이 in (A, B, C, ...)에 있는 값과 동일한 값들을 조회  
where 칼럼 not in (A, B, C, ...) : 칼럼의 값이 in(A, B, C, ...)에 있는 값과 동일하지 않은 값들을 조회

- EMP 테이블에서 업무(job)가 'IT_PROG' 거나 'ST_MAN' 인 직원의  ID(emp_id), 이름(emp_name), 업무(job)을 조회

```sql
select emp_id 직원ID, emp_name 이름, job 업무 from emp where job in ('IT_PROG', 'ST_MAN');
```

###### 결과

![결과2-5](/image_file/결과2-5.png)

- EMP 테이블에서 업무(job)가 'IT_PROG' 나 'ST_MAN' 가 아닌 직원의  ID(emp_id), 이름(emp_name), 업무(job)을 조회

```sql
select emp_id 직원ID, emp_name 이름, job 업무 from emp where job not in ('IT_PROG', 'ST_MAN');
```

###### 결과

![결과2-6](/image_file/결과2-6.png)

****

4. where 컬럼 like 패턴 : 칼럼의 값들 중 패턴이 일치하는 값들을 조회  
where 컬럼 not like 패턴 : 칼럼의 값들 중 패턴이 일치하지 않는 값들을 조회
- % : 문자열을 의미, _ : 한 개의 문자를 의미  
ex) 'AB%' : AB로 시작하는 문자열, 'AB%' : AB로 끝나는 문자열, '%AB%' : 중간에 AB가 들어있는 문자열  
ex) '__AB%' : 두 글자 뒤에 AB가 나오고 그 뒤에 문자열이 나오는 패턴

- EMP 테이블에서 직원 이름(emp_name)이 en으로 끝나는 직원의  ID(emp_id), 이름(emp_name)을 조회

```sql
select emp_id 직원ID, emp_name 이름 from emp where emp_name like '%en';
```

###### 결과

![결과2-7](/image_file/결과2-7.png)

- EMP 테이블에서 직원 이름(emp_name)이 S로 시작하지 않는 직원의  ID(emp_id), 이름(emp_name)

```sql
select emp_id 직원ID, emp_name 이름 from emp where emp_name NOT LIKE 'S%';
```

###### 결과

![결과2-8](/image_file/결과2-8.png)

- EMP 테이블에서 직원 이름(emp_name)의 세 번째 문자가 “e”인 모든 사원의 이름을 조회

```sql
select emp_name 직원이름 from emp where emp_name like '__e%';
```

###### 결과

![결과2-9](/image_file/결과2-9.png)

****

5. null의 비교는 = 또는 != 연산으로 안된다. is 또는 is not을 사용한다.  
where 컬럼 is null : 컬럼의 값 중에 null인 값들을 조회  
where 컬럼 is not null : 컬럼의 값 중에 null이 아닌 값들을 조회

- EMP 테이블에서 부서명(dept_name)이 null인 직원의 ID(emp_id), 이름(emp_name), 부서명(dept_name)을 조회

```sql
select emp_id 직원ID, emp_name 이름, dept_name 부서명 from emp where dept_name is null;
```

###### 결과

![결과2-10](/image_file/결과2-10.png)

- 부서명(dept_name) 이 NULL이 아닌 직원의 ID(emp_id), 이름(emp_name), 부서명(dept_name) 조회

```sql
select emp_id 직원ID, emp_name 이름, dept_name 부서명 from emp where dept_name is not null;
```

###### 결과

![결과2-11](/image_file/결과2-11.png)

****

6. where의 조건이 여러개인 경우 and 또는 or 을 사용한다.

- EMP 테이블에서 업무(job)가 'SA_REP' 이고 급여(salary)가 $9,000 인 직원의 직원의 ID(emp_id), 이름(emp_name), 업무(job), 급여(salary)를 조회

```sql
select emp_id 직원ID, emp_name 이름, job 업무, salary 급여 from emp where job = 'SA_REP' AND salary = 9000;
```

###### 결과

![결과2-12](/image_file/결과2-12.png)

- EMP 테이블에서 업무(job)에 'MAN'이 들어가는 직원들 중 급여(salary)가 $10,000 이하이 거나 2008년 이후 입사한  
직원의 ID(emp_id), 이름(emp_name), 업무(job), 입사일(hire_date), 급여(salary)를 조회

```sql
select emp_id 직원ID, emp_name 이름, job 업무, hire_date 입사일, salary 급여 from emp
where job like '%MAN%' AND salary <= 10000 OR hire_date >= '2008/01/01';
```

###### 결과

![결과2-13](/image_file/결과2-13.png)

****

### SELECT 컬럼 FROM 테이블명 WHERE 조건 ORDER BY 컬럼

1. ORDER BY 컬럼 : 해당 컬럼에 있는 값들을 정렬 (디폴트는 오름차순)

- 부서명을 부서명(dept_name)의 오름차순으로 정렬해서 조회(중복은 제거)

```sql
select DISTINCT dept_name from emp order by dept_name;
```

###### 결과

****

![결과2-14](/image_file/결과2-14.png)

2. ORDER BY 컬럼 ASC : 해당 컬럼에 있는 값들을 오름차순으로 정렬 ( 숫자 -> 대문자 -> 소문자 -> 한글 -> null )  
ORDER BY 컬럼 DESC : 해당 컬럼에 있는 값들을 내림차순으로 정렬 ( null -> 한글 -> 소문자 -> 대문자 -> 숫자 )  

- 부서명을 부서명(dept_name)의 오름차순으로 정렬해서 조회(중복은 제거)

```sql
select DISTINCT dept_name from emp order by dept_name asc;
```

###### 결과

![결과2-14](/image_file/결과2-14.png)

- 부서명을 부서명(dept_name)의 내림차순으로 정렬해서 조회(중복은 제거)


```sql
select DISTINCT dept_name from emp order by dept_name desc;
```

###### 결과

![결과2-15](/image_file/결과2-15.png)

****

3. nulls first : 오름차순에서 null이 먼저 나오도록 한다.  
nulls last : 내림차순에서 null을 마지막에 나오도록 한다.

- 부서명을 부서명(dept_name)의 오름차순으로 정렬해서 조회(중복은 제거, null인 경우 가장 먼저 나온다.)

```sql
select DISTINCT dept_name from emp order by dept_name nulls first;
```

###### 결과

![결과2-17](/image_file/결과2-17.png)

- 부서명을 부서명(dept_name)의 내림차순으로 정렬해서 조회(중복은 제거, null인 경우 가장 나중에 나온다.)

```sql
select DISTINCT dept_name from emp order by dept_name desc nulls last;
```

###### 결과

![결과2-18](/image_file/결과2-18.png)

****

4. 날짜의 경우  
오름차순 : 과거 -> 미래  
내림차순 : 미래 -> 과거

- EMP 테이블에서 직원의 ID(emp_id), 이름(emp_name), 업무(job), 입사일(hire_date)을 입사일(hire_date) 순(내림차순)으로 조회

```sql
select emp_id 직원ID, emp_name 이름, job 업무, hire_date 입사일 from emp order by hire_date desc;
```

###### 결과

![결과2-16](/image_file/결과2-16.png)

****

5. SELECT 컬럼 FROM 테이블명 WHERE 조건 ORDER BY 컬럼

- 급여(salary)가 $5,000을 넘는 직원의 ID(emp_id), 이름(emp_name), 급여(salary)를 급여가 낮은 순서부터 조회

```sql
select emp_id 직원ID, emp_name 이름, salary 급여 from emp where salary > 5000 order by salary;
```

###### 결과

![결과2-19](/image_file/결과2-19.png)

****

6. SELECT 컬럼 FROM 테이블명 WHERE 조건 ORDER BY 컬럼1 (ASC or DESC), 컬럼2 (ASC or DESC), ...  
1차로 컬럼1로 정렬을 하고, 컬럼1에서 동일한 값이 존재할 경우 2차로 컬럼2로 정렬을 하고, ...

- 직원들의 id(emp_id), 이름(emp_name), 업무(job), 급여(salary)를  
업무(job) 순서대로 (A -> Z) 조회하고 업무(job)가 같은 직원들은  급여(salary)가 높은 순서대로 2차 정렬해서 조회

```sql
select emp_id 직원ID, emp_name 이름, job 업무, salary 급여 from emp order by job, salary DESC;
```

###### 결과

![결과2-20](/image_file/결과2-20.png)

- EMP 테이블에서 ID(emp_id), 이름(emp_name), 급여(salary), 입사일(hire_date)을  
급여(salary) 내림차순으로 정렬하고 급여(salary)가 같은 경우는 입사일(hire_date)가 오래된 순서로 정렬

```sql
select emp_id 직원ID, emp_name 이름, salary 급여, hire_date 입사일 from emp order by salary desc, hire_date asc;
```

###### 결과

![결과2-21](/image_file/결과2-21.png)

****




