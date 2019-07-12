

### ROLLUP
- 중간집계, 총집계를 group 별 부분집계에 추가해서 보려고 할 때 사용
- select ex1, ex2, ... , 집계함수(expr)  
from 테이블  
group by rollup(ex1, ex2, ...)  
(ex1, ex2, ..., expr => 컬럼)  
rollup의 결과 : 집계에 참여한 컬럼의 값은 null이 , expr 컬럼에 집계결과가 나온다.
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
      
- 중간집계 또는 총집계의 결과는 그룹함수에 의해 결정된다.  
i. 예제의 경우 그룹함수가 avg()였으므로, 총집계의 결과도 avg()인 전체의 평균으로 나온다.  
ii. 예제의 경우 그룹함수가 sum()과 count()였으므로,  
중간집계와 총집계의 결과 또한 sum()인 전체의 합과 count()인 전체 갯수의 결과가 나온다.  
아래 예제의 경우 그룹함수가 max()와 min()이므로, 총집계의 결과 또한 max()인 전체 최댓값과 min()인 전체 최솟값이 나온다.
  - 예제)  
    부서별(dept_name) 별 최대 salary와 최소 salary와 전체 최대 salary와 최소 salary를 조회  
    
    ```sql
    select dept_name 부서, max(salary) 최대급여, min(salary) 최소급여
    from emp
    group by rollup(dept_name);
    ```
    
    ###### 결과
    
    ![결과13-17](/image_file/결과13-17.png)
    
****
    
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
   
    ****
    
### GROUPING
- select grouping(group_by에서 사용한 컬럼명)  
=> grouping()의 인자로는 컬럼이 한 개만 올 수 있다.
- group by 에서 rollup이나 cube로 묶은 컬럼의 행이 집계시 참여 했으면 1, 집계시 참여하지 않았으면 0을 반환한다.
- 전체 집계에 나오는 (null)대신 다른 값을 넣을 때 사용
- 예시)  
  EMP 테이블에서 업무(JOB) 별 급여(salary)의 평균과 평균의 총계도 같이나오도록 조회  
  
  ```sql
  select dept_name 업무,
       grouping(dept_name) grouping,
       ceil(avg(salary)) 평균급여
       from emp
       group by rollup(dept_name);
  ```
  
  ###### 결과
  
  ![결과13-7](/image_file/결과13-7.png)
  
  EMP 테이블에서 업무(JOB) 별 급여(salary)의 평균과 평균의 총계도 같이나오도록 조회  
  (업무 컬럼에  소계나 총계이면 '총평균'을  일반 집계이면 업무(job)을 출력)
  
  ```sql
  select decode(grouping(dept_name), 0, dept_name, '총평균') 업무,
       ceil(avg(salary)) 평균급여
       from emp
       group by rollup(dept_name);
  ```
  
  ###### 결과
  
  ![결과13-8](/image_file/결과13-8.png)
  
  ****
  
### GROUPING_ID
- select grouping_id(group_by에서 사용한 컬럼명)  
=> grouping_id()의 인자로는 컬럼이 여러 개 올 수 있다.
- grouping_id()는 2진수를 10진수로 변환한 결과가 나온다.
  1. grouping_id()의 인자로 한 개의 컬럼만 올 경우  
     => grouping()과 동일한 결과가 나온다.
  - 예시)  
    EMP 테이블에서 업무(JOB) 별 급여(salary)의 평균과 평균의 총계도 같이나오도록 조회  
  
    ```sql
    select dept_name 업무,
    grouping_id(dept_name) grouping_id,
    ceil(avg(salary)) 평균급여
    from emp
    group by rollup(dept_name);
    ```
    
    ###### 결과
    
    ![결과13-9](/image_file/결과13-9.png)
    
  2. grouping_id()의 인자로 두 개 이상의 컬럼이 올 경우  
     - grouping_id(a, b)  
     grouping_id(b)는 grouping_id(a, b)에서 2진수의 1번째 인자가 된다.  
     grouping_id(a)는 grouping_id(a, b)에서 2진수의 2번째 인자가 된다.  
     grouping_id(a, b)는 grouping(a)와 grouping(b)의 결과를 합친 2진수를 10진수로 바꿔서 나온다.  
     - grouping_id(a, b)의 결과는 0, 1, 3으로 나온다.  
     - grouping_id(a, b, c)의 결과는 0, 1, 3, 7로 나온다.
     - 예시)  
       부서별(dept_name), 입사년도별 평균 급여(salary) 조회. 부서별 집계와 총집계가 같이 나오도록 조회
     
       ```sql
       select dept_name 부서,
       to_char(hire_date,'yyyy') 입사년도,
       grouping_id(dept_name)"grouping_id(a)",
       grouping_id(to_char(hire_date,'yyyy')) "grouping_id(b)",
       grouping_id(dept_name, to_char(hire_date, 'yyyy')) "grouping_id(a, b)",
       round(avg(salary)) 평균급여
       from emp
       group by rollup(dept_name, to_char(hire_date, 'yyyy'));
       ```
       
       ###### 결과
       
       ![결과13-10](/image_file/결과13-10.png)
       ![결과13-11](/image_file/결과13-11.png)
       ![결과13-12](/image_file/결과13-12.png)
       
       부서별(dept_name), 입사년도별 평균 급여(salary) 조회. 부서별 집계와 총집계가 같이 나오도록 조회
       부서 컬럼에 총집계이면 '총평균'을 입사년도 컬럼에 중간집계이면 '중간평균'을 출력
       
       ```sql
       select decode(grouping_id(dept_name), 0, dept_name, '총평균') 부서,
       decode(grouping_id(dept_name, to_char(hire_date, 'yyyy')),
              0, to_char(hire_date, 'yyyy'),
              1, '중간평균',
              ' ') 입사년도,
       round(avg(salary)) 평균급여
       from emp
       group by rollup(dept_name, to_char(hire_date, 'yyyy'));
       ```
  
       ###### 결과
       
       ![결과13-13](/image_file/결과13-13.png)  
       ![결과13-14](/image_file/결과13-14.png)
       
       EMP 테이블에서 부서(dept_name), 업무(job) 별 salary의 합계와 직원수를 중간집계와 총집계가 나오도록 조회
       
       ```sql
       select decode(grouping_id(dept_name), 0, dept_name, '총집계') 부서,
       decode(grouping_id(dept_name, job), 0, job, 1, '중간집계', 3, ' ') 업무,
       sum(salary) 총급여,
       count(*) 직원수
       from emp
       group by rollup(dept_name, job);
       ```
       ###### 결과
       
       ![결과13-15](/image_file/결과13-15.png)  
       ![결과13-16](/image_file/결과13-16.png)
  
****
