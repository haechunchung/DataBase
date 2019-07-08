
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
