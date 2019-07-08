
### DESC 테이블명
- 테이블의 구조를 보여준다.

``` sql
desc emp;
```
###### 결과
![emp테이블구조](/image_file/emp테이블구조.png)


### SELECT 컬럼, 컬럼, ... FROM 테이블명
1. 테이블의 모든 항목을 조회할 때는 * 를 사용한다.  
- EMP 테이블의 모든 컬럼의 모든 항목을 조회
```sql
select * from emp;
```

2. select 컬럼, 컬럼, ... from 테이블명
- EMP 테이블의 직원 ID(emp_id), 직원 이름(emp_name), 업무(job) 컬럼의 값을 조회

```sql
select emp_id, emp_name, job from EMP;
```

###### 결과
![결과1-1](/image_file/결과1-1.png)

3. DOSTINCT는 조회된 내용에서 중복을 제거해 준다.
- EMP 테이블의 업무(job) 어떤 값들로 구성되었는지 조회 - 동일한 값은 하나씩만 조회되도록 처리  


```sql
select DISTINCT job from EMP;
```

###### 결과
![결과1-2](/image_file/결과1-2.png)

4. DISTINCT는 조회하는 모든 컬럼에 적용된다.(하나의 컬럼에만 적용되지 않는다.)  
EMP테이블에서 emp_id가 Primary key이므로 중복이 없다. 따라서 위의 2번과 결과가 같다.

```sql
select DISTINCT emp_id, emp_name, job from EMP;
```

###### 결과
![결과1-1](/image_file/결과1-1.png)

5. select 컬럼 as 별칭 from 테이블명 (as는 생략가능)  
=> 컬럼의 제목을 별칭으로 나타내서 보여준다.  
=> 만약 별칭에 띄어쓰기가 있을 경우 반드시 쌍따옴표로 묶어주어야 한다.  
- EMP 테이블에서 emp_id는 직원 ID, emp_name은 직원이름, hire_date는 입사일, salary는 급여, dept_name은 소속부서 별칭으로 조회

```sql
select emp_id "직원 ID", emp_name 직원이름, hire_date 입사일, salary 급여, dept_name 소속부서 from EMP;
```

###### 결과
![결과1-3](/image_file/결과1-3.png)
