# JDBC

## 개요

자바에서 데이터베이스에 접근할 수 있게 해주는 Programming API

`Application` -> `JDBC Interface` -> `DB Server`

java.sql 패키지 내에 해당 API가 포함되어있음

### API 추가 방법

1. OJDBC 다운로드

  - [Oracle 홈페이지](http://www.oracle.com)에 가서 맞는 버전(ex. ojdbc6.jar) 다운

  - Oracle에서 복사(oracle 설치 ex. \product\11.2.0\server\jdbc\lib\ojdbc6) Ctrl + C, V

2. OJDBC 파일을 JDK에 넣기

  - 경로 : 설치 폴더\jre\lib\ext

3. Library 등록

  - Properties에서 등록 가능(Properties -> Java Build Path -> Add External JARs -> ojdbc6.jar)
    -> Referenced Libraries에 ojdbc6.jar 생성됨


### 사용 객체

- DriverManager

데이터 원본에 JDBC Driver를 통하여 Connection을 생성하는 역할.

`Class.forName()`메소드를 통해 생성되며, **반드시** 예외처리를 해야 함.

직접 객체 생성이 불가능하며, `getConnection()` 메소드를 활용

- Connection

데이터 원본과 연결된 커넥션으로, Statement 객체를 생성할 때 Connection 객체를 사용하여 `createStatement()` 메소드 생성 후 호출

- Statement & PreparedStatement

  - Statement : Connection 객체의 `createStatement()` 메소드를 호출하여 생성
  
    `executeQuery()` 또는 `executeUpdate()` 를 통해 SQL 쿼리문 실행

  - PreparedStatement : Connection 객체의 `preparedStatement()` 메소드를 호출하여 생성

    SQL 쿼리문이 컴파일 되고 실행기간 동안 인수값을 위한 공간을 확보하며, 각각 인수의 위치에 `?`를 사용하여 SQL 문장 정의

- ResultSet

  SELECT문을 사용한 질의 성공시 Result Set 반환함

### Statement 활용법

```java
// student 계정의 employee 라는 계정의 데이터를 불러온다고 가정
import Test.*;

public class Test {
    public static void main(String[] args) {
        Test t = new Test();
        t.selectAll();
    }

    public void selectAll() { // student 계정의 employee 테이블 전체를 조회해서 출력하는 메소드
        Connection conn = null; // Connection 객체 정의
        Statement stmt = null; // Statement 객체 정의
		ResultSet rset = null; // ResultSet 객체 정의
		
        // SQL 쿼리문 정의 : employee 테이블 데이터 불러오기
		String query = "select * from employee";
		
		try {
			Class.forName("oracle.jdbc.driver.OracleDriver"); // Connection을 생성(!ClassNotFOundException 반드시 생성)
			// Connection 객체를 통해 Oracle DB에 접근(ID:student, PWD:student)(!SQLException 반드시 생성)
            conn = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:xe", "student", "student");
			
			stmt = conn.createStatement(); // createStatement()를 통해 connection 객체의 내용 생성
			rset = stmt.executeQuery(query); // 쿼리문을 활용하여 ResultSet에 담기
			
			while(rset.next()) { // next()를 활용해 ResultSet의 다음 데이터에 접근
				System.out.println(rset);
			}
		} catch (ClassNotFoundException | SQLException e) {
			e.printStackTrace();
		} finally {
			try { // JDBC 관련 객체 Close
				rset.close(); 
				stmt.close();
				conn.close();
			} catch (SQLException e) {
				e.printStackTrace();
			}
		}
	}
}
```

### PreparedStatement 활용법

```java
public void selectOne(int empId) {
    Connection conn = null;
    PreparedStatement pstmt = null;
    ResultSet rset = null;

    try {
        Class.forName("oracle.jdbc.driver.OracleDriver");
        conn = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:xe", "student", "student");
        
        String query = "select * from employee where emp_id = ?"; // 인수의 위치에 '?'를 활용하여 쿼리문 생성
        pstmt = conn.prepareStatement(query); // prepareStatement()를 통해 쿼리문을 불러온 뒤 인수를 불러올 공간 확보
        pstmt.setInt(1, empId); // setInt()를 통해 인수의 위치 '1'에 empId로 설정해줌
        rset = pstmt.executeQuery(); // Resultset 객체에 최종 확인할 쿼리문 넣기
        
        while(rset.next()) {
            System.out.println(rset);
        
        }
    } catch (ClassNotFoundException | SQLException e) {
        e.printStackTrace();
    } finally {
        try {
            rset.close();
            // stmt.close();
            pstmt.close();
            conn.close();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

