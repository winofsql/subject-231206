# subject-231206

### [🔴 ChatGPT への質問](https://chat.openai.com/share/584803be-ffc1-4b05-9c11-0dfd94e690a3)

### Windows 用 sqlite3 ダウンロード 
![image](https://github.com/winofsql/subject-231206/assets/1501327/1cecedea-d381-442c-b03b-ac36f1440a56)
[sqlite-tools-win-x64-バージョン.zip](https://www.sqlite.org/download.html)


### Java テンプレートのメニューから基本コード
![image](https://github.com/winofsql/subject-231206/assets/1501327/5fda0e69-fdd2-464f-9354-4be2b36d705f)

MySQL 用接続文字列
```
"jdbc:mysql://localhost/lightbox?user=root&password=&characterEncoding=UTF-8"
```

```java
package action;

import java.sql.*;
import javax.swing.*;
import java.io.*;

public class AppWindow extends BaseWindow {

    private Connection conn = null;
    private Statement stmt = null;
    private ResultSet rs = null;

    private JPanel jContentPane = null;
    private JButton jButton = null;

    // 社員コード
    private JLabel lblScode = null;
    private JTextField jScode = null;

    // 氏名
    private JLabel lblSname = null;
    private JTextField jSname = null;

    // フリガナ
    private JLabel lblFuri = null;
    private JTextField jFuri = null;

    // 性別
    private JLabel lblSeibetu = null;
    private JTextField jSeibetu = null;

    private JComboBox<String> genderComboBox;
    // private int[] genders = {0, 1};
    private String[] genderLabels = {"男性", "女性"};

    public int mainWidth = 600;
    public int mainHeight = 400;
    public String titleString = "Swing 簡易サンプル";

    // *****************************************************
    // ボタン作成とクリックイベント
    // *****************************************************
    private JButton getJButton() {
        if (jButton == null) {
            jButton = new JButton();
            // メインウインドウに対して、100x22 のボタンを追加
            jButton.setBounds( 250, 30-3, 100, 22 );
            jButton.setText("実行");
            jButton.addActionListener(new java.awt.event.ActionListener() {
                public void actionPerformed(java.awt.event.ActionEvent e) {

                    try {
                        conn = DriverManager.getConnection(
                            "jdbc:mysql://localhost/lightbox?user=root&password=&characterEncoding=UTF-8"
                        );

                        // ステートメント
                        stmt = conn.createStatement();
                        // SQL 実行
                        String sCode = jScode.getText();
                        rs = stmt.executeQuery("select * from 社員マスタ where 社員コード = '" + sCode + "'");

                        // 一行取り出し
                        rs.next();

                        // 社員名
                        String sName = rs.getString("氏名");
                        jSname.setText(sName);

                        // 社員名
                        String sFuri = rs.getString("フリガナ");
                        jFuri.setText(sFuri);


                        // 整数
                        int seibetu = rs.getInt("性別");
                        jSeibetu.setText(seibetu+"");
                        genderComboBox.setSelectedIndex(seibetu);

                        // 文字列
                        String seibetu2 = String.format("%d", seibetu);
                        if ( seibetu2.equals("0") ) {
                            System.out.println("男性");
                        }
                        else {
                            System.out.println("女性");
                        }

                        rs.close();
                        stmt.close();
                        conn.close();

                    }
                    catch (Exception ex) {
                        System.out.println( ex.getMessage() );
                        ex.printStackTrace();
                    }

                    // 編集状態の切り替え
                    jScode.setEditable(false);
                    jSname.setEditable(true);
                    jFuri.setEditable(true);
                    genderComboBox.setEnabled(true);

                }
            });
        }
        return jButton;
    }

    // *****************************************************
    // コンストラクタ
    // *****************************************************
    public AppWindow() {
        super();
        initialize();
    }

    // *****************************************************
    // 初期処理
    // *****************************************************
    private void initialize() {
        // ウインドウサイズの決定
        this.setSize(mainWidth, mainHeight);

        // ウインドウ位置の変更
        centerWindow();

        // パネルを適用
        this.setContentPane(getJContentPane());

        // タイトルセット
        this.setTitle(titleString);

        // カレントディレクトリの表示
        File cur = new File("");
        System.out.println(cur.getAbsolutePath());
    }

    // *****************************************************
    // 画面( パネル作成 )
    // *****************************************************
    private JPanel getJContentPane() {

        if (jContentPane == null) {
            jContentPane = new JPanel();
            jContentPane.setLayout(null);
            jContentPane.add(getJButton(), null);

            lblScode = new JLabel("社員コード");
            lblScode.setBounds(60, 30, 80, 19);
            jContentPane.add(lblScode);

            jScode = new JTextField();
            jScode.setBounds(150, 30, 60, 19);
            jContentPane.add(jScode);

            lblSname = new JLabel("氏名");
            lblSname.setBounds(60, 30+50, 80, 19);
            jContentPane.add(lblSname);

            jSname = new JTextField();
            jSname.setBounds(150, 30+50, 120, 19);
            jContentPane.add(jSname);

            lblFuri = new JLabel("フリガナ");
            lblFuri.setBounds(60, 30+50+30, 80, 19);
            jContentPane.add(lblFuri);

            jFuri = new JTextField();
            jFuri.setBounds(150, 30+50+30, 120, 19);
            jContentPane.add(jFuri);

            lblSeibetu = new JLabel("性別");
            lblSeibetu.setBounds(60, 30+50+30+30, 80, 19);
            jContentPane.add(lblSeibetu);

            // 非表示の性別テキストフィールド
            jSeibetu = new JTextField();
            jSeibetu.setBounds(150, 30+50+30+30, 30, 19);
            jContentPane.add(jSeibetu);
            jSeibetu.setVisible(false);

            genderComboBox = new JComboBox<>(genderLabels);
            genderComboBox.setBounds(150, 30+50+30+30, 150, 19);
            jContentPane.add(genderComboBox);


            // 初期状態の画面制御
            jSname.setEditable(false);
            jFuri.setEditable(false);
            genderComboBox.setEnabled(false);

        }
        return jContentPane;
    }

}
```
