

### ROLLUP
- 중간집계, 총집계를 group 별 부분집계에 추가해서 보려고 할 때 사용
- select ex1, ex2, ... , 집계함수(expr)  
from 테이블  
group by rollup(ex1, ex2, ...)  
(ex1, ex2, ..., expr => 컬럼)  
rollup의 결과는 집계에 참여한 컬럼의 값은 null이 나오고 expr에 집계결과가 나온다.
- rollup 집계 방법
  1. group by rollup(컬럼)  
    컬럼에 대해 group by를 진행한 후,  
    마지막에 null과 집계결과가 나온다.  
      
    - 예시)  
      EMP 테이블에서 업무(job) 별 급여(salary)의 평균과 평균의 총계도 같이나오도록 조회  
    
      ```sql
      select job 업무, ceil(avg(salary)) 평균급여
      from emp
      group by rollup(job);
      ```
    
      ###### 결과
    
      ![결과13-1](/image_file/결과13-1.png)
    
    2. group by rollup(a, b)  
      1.  
      (a1, b1), (a1, b2), ... : a1(첫번째 컬럼의 첫번째 그룹) 내에서 b(두번째 컬럼)의 다른 그룹들을 다 합쳐서 집계  
      (a2, b1), (a2, b2), ... : a2(첫번째 컬럼의 두번째 그룹) 내에서 b(두번째 컬럼)의 다른 그룹들을 다 합쳐서 집계  
      => a(첫번째 컬럼)의 그룹의 개수만큼 진행  
      => 중간중간 집계 결과가 나온다.  
      2.  
      a(첫번째 컬럼)에 해당하는 모든 그룹을 집계 (전체 집계)
      
    - 예시)  
      EMP 테이블에서 부서(dept_name), 업무(job) 별 salary의 합계와 직원수를 소계와 총계가 나오도록 조회  
    
      ```sql
      select dept_name 부서, job 업무, sum(salary) 총급여, count(*) 직원수
      from emp
      group by rollup(dept_name, job);
      ```
    
      ###### 결과
    
      ![결과13-2](/image_file/결과13-2.png)  
      ![결과13-3](/image_file/결과13-3.png)
    
### CUBE
- rollup의 확장판
- 나올 수 있는 모든 그룹에 대한 집계를 한다.
- 그룹으로 묶는 컬럼이 하나일 경우 rollup과 효과가 동일하다.  
=> 차이점 : 총집계가 rollup은 맨아래 나오고, cube는 맨위에 나온다.  
- 잘 사용하지 않는다.
- cube 집계 방법
  1. group by cube(컬럼)  
  rollup과 동일하다.  
  => 다만, 총집계가 맨 위에 나온다.  
  
  - 예시)  
    EMP 테이블에서 업무(job) 별 급여(salary)의 평균과 평균의 총계도 같이나오도록 조회  
    
    ```sql
    select job 업무, ceil(avg(salary)) 평균급여
    from emp
    group by cube(job);
    ```
    
    ###### 결과
    
    ![결과13-4](/image_file/결과13-4.png)
    
  2. group by rollup(a, b)  
      1.  
      (a1, b1), (a1, b2), ... : a1(첫번째 컬럼의 첫번째 그룹) 내에서 b(두번째 컬럼)의 다른 그룹들을 다 합쳐서 집계  
      (a2, b1), (a2, b2), ... : a2(첫번째 컬럼의 두번째 그룹) 내에서 b(두번째 컬럼)의 다른 그룹들을 다 합쳐서 집계  
      => a(첫번째 컬럼)의 그룹의 개수만큼 진행  
      => 중간중간 집계 결과가 나온다.  
      2.  
      (b1, a1), (b1, a2), ... : b1(두번째 컬럼의 첫번째 그룹) 내에서 a(첫번째 컬럼)의 다른 그룹들을 다 합쳐서 집계  
      (b2, a1), (b2, a2), ... : b2(두번째 컬럼의 두번째 그룹) 내에서 a(첫번째 컬럼)의 다른 그룹들을 다 합쳐서 집계  
      => b(두번째 컬럼)의 그룹의 개수만큼 진행  
      => b에 대한 집계이므로 첫번째컬럼인 a가 null이 나온다.  
      => 따라서 위에 한번에 몰아서 나온다.  
      3.  
      a(첫번째 컬럼)에 해당하는 모든 그룹을 집계(전체 집계)  
      => b(두번째 컬럼)에 해당하는 모든 그룹으로 집계를 해도 전체 집계로 동일하므로 하나만 나온다.
      
    - 예시)  
      EMP 테이블에서 부서(dept_name), 업무(job) 별 salary의 합계와 직원수를 소계와 총계가 나오도록 조회  
    
      ```sql
      select dept_name 부서, job 업무, sum(salary) 총급여, count(*) 직원수
      from emp
      group by rollup(dept_name, job);
      ```
    
      ###### 결과
    
      ![결과13-5](/image_file/결과13-5.png)  
      ![결과13-6](/image_file/결과13-6.png)
    
### GROUPING
