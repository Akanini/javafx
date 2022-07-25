# javafx
	
NEW ANNOUNCEMENT
LOGIN CLASS


public class GUI_New_Window extends Application {

    @Override
    public void start(Stage primaryStage) {
        Text name_lbl = new Text("User Name");
        Text pass_lbl = new Text("Password");

        TextField uname_tf = new TextField();
        PasswordField pass = new PasswordField();

        Button login_btn = new Button("Login");
        Button clear_btn = new Button("Clear");
        final ImageView selectedImage = new ImageView();

        Image image1 = new Image(GUI_New_Window.class.getResourceAsStream("img.png"));

        selectedImage.setImage(image1);
        selectedImage.setX(10);
        selectedImage.setY(10);
        selectedImage.setFitWidth(50);
        selectedImage.setPreserveRatio(true);

        GridPane gridPane = new GridPane();
        gridPane.setMinSize(600, 300);
        gridPane.setVgap(10);
        gridPane.setHgap(20);
        gridPane.setAlignment(Pos.CENTER);

        gridPane.add(name_lbl, 1, 1);
        gridPane.add(pass_lbl, 1, 2);
        gridPane.add(login_btn, 1, 3);

        gridPane.add(uname_tf, 2, 1);
        gridPane.add(pass, 2, 2);
        gridPane.add(clear_btn, 2, 3);
        gridPane.add(selectedImage, 1, 0);

        login_btn.setOnMouseClicked((new EventHandler<MouseEvent>() {
            public void handle(MouseEvent event) {

                String username = uname_tf.getText();
                String password = pass.getText();
                try {
                    //Step One - Register the driver
                    Class.forName("com.mysql.cj.jdbc.Driver");

                    //Step Two - Creating the connection
                    Connection con = DriverManager.getConnection("jdbc:mysql://127.0.0.1/exercise?", "root", "");

                    //Step Three - Create the statement object
                    Statement st = con.createStatement();

                    //Step Four - Execute your queries
                    String query = "SELECT * FROM exercise.users Where username = '" + username + "' AND password = '" + password + "' ";
                    ResultSet rs = st.executeQuery(query);
                    //Boolean h = true;                

                    if (rs.next()) {
                        gui_two g2 = new gui_two();
                        g2.start(gui_two.secondGuiStage);
                    }                    
                    else
                    {
                        Alert al = new Alert(Alert.AlertType.WARNING);
                        al.setContentText("Invalid Credentials");
                        al.show();
                       
                    }
               

                } catch (Exception ee) {
                    System.out.println(ee);
                    System.out.println("Connection error");
                    //You can replace this code with ANY code to be executed after a unsuccessfull connection
                    Alert alert = new Alert(Alert.AlertType.ERROR);
                    alert.setContentText("Check your Database Connection");
                    alert.show();
                }
            }
               }));
       
                clear_btn.setOnMouseClicked((new EventHandler<MouseEvent>() {
                     public void handle(MouseEvent event) {
                      uname_tf.setText("");
                      pass.setText("");                      
                     
                     }
                  }));

            primaryStage.setTitle ("Login GUI");      
            Scene scene = new Scene(gridPane);
            primaryStage.setScene (scene);
            primaryStage.show ();
        } /**
                 * @param args the command line arguments
                 */

    public static void main(String[] args) {
        launch(args);
    }

}
