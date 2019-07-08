

### SELECT 컬럼 FROM 테이블명 WHERE 조건  
1. 숫자, 문자열 모두 >, >=, <, <=, =, != 비교

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

3. where 칼럼 in (A, B, ...) : 칼럼의 값이 in (A, B, ...)에 있는 값과 동일한 값들을 조회  
where 칼럼 not in (A, B, ...) : 칼럼의 값이 in(A, B, ...)에 있는 값과 동일하지 않은 값들을 조회

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

