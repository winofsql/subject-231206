### Java テンプレート

- ### 初期状態
  ![image](https://github.com/winofsql/subject-231206/assets/1501327/b6b1a6b3-b02f-487a-a7a5-de8b11219aae)

  ![image](https://github.com/winofsql/subject-231206/assets/1501327/8db8b8ef-0b8d-4245-8d48-9c063c95805e)


- ### sqlite3 パッケージ
  ![image](https://github.com/winofsql/subject-231206/assets/1501327/58599302-d4cf-4920-afed-ca4b8c5165fc)

  ![image](https://github.com/winofsql/subject-231206/assets/1501327/7268875b-7998-4bdb-be75-d1bfd16e60c1)

  ![image](https://github.com/winofsql/subject-231206/assets/1501327/a46343be-4256-4603-ba12-ea51000ff087)

- ### lightbox.sqlite3 取得
  ![image](https://github.com/winofsql/subject-231206/assets/1501327/8690da13-fe61-443c-b565-8df2876821d4)
  ```
  wget -O lightbox.sqlite3 https://github.com/winofsql/resource-winofsql/raw/main/sqlite3/lightbox.sqlite3
  ```

  ```java
  import java.sql.*;

  class Main {
    public static void main(String[] args) {
  
      String dbname = "lightbox.sqlite3";
      Connection conn = null;
      Statement stmt = null;
      try {
  
        conn = DriverManager.getConnection("jdbc:sqlite:" + dbname);
  
        stmt = conn.createStatement();
  
        ResultSet rs = stmt.executeQuery("SELECT * FROM 社員マスタ");
        while (rs.next()) {
           String name = rs.getString("氏名");
           System.out.println(name); // 取得したデータを表示
        }
        rs.close();
  
      } catch (Exception e) {
        e.printStackTrace();
      }
    }
  }
  ```
