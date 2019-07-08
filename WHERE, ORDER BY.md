

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

6. 
