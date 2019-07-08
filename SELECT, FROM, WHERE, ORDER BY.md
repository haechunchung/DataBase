
### DESC 테이블명
- 테이블의 구조를 보여준다.

``` sql
desc emp;
```
###### 결과
![emp테이블구조](/image_file/emp테이블구조.png)


### SELECT 컬럼, 컬럼, ... FROM 테이블명
- 테이블의 모든 항목을 조회할 때는 * 를 사용한다.

```sql
select * from emp;
```

- EMP 테이블의 직원 ID(emp_id), 직원 이름(emp_name), 업무(job) 컬럼의 값을 조회

```sql
select emp_id, emp_name, job from EMP;
```

###### 결과
![결과1-1](/image_file/결과1-1.png)

- EMP 테이블의 업무(job) 어떤 값들로 구성되었는지 조회 - 동일한 값은 하나씩만 조회되도록 처리

```sql
select DISTINCT job from EMP;
```

###### 결과
