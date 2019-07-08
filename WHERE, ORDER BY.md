

### SELECT 컬럼 FROM 테이블명 WHERE 조건  
1. 숫자, 문자열 모두 >, >=, <, <=, =, != 비교

- EMP 테이블에서 직원_ID(emp_id)가 110인 직원의 이름(emp_name)과 부서명(dept_name)을 조회

```sql
select emp_name 직원이름, dept_name 부서명 from EMP where emp_id = 110;

```

###### 결과


- EMP 테이블에서 'IT' 부서에 속하는 직원들의 ID(emp_id), 이름(emp_name), 부서명(dept_name)을 조회

```sql
select emp_id 직원ID, emp_name 이름, dept_name 부서명 from EMP where dept_name = 'IT';
```

###### 결과

