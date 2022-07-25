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

	
NEW ANNOUNCEMENT
SECOND GUI


public class gui_two extends Application {
   
    static Stage secondGuiStage = new Stage();

    @Override
           
    public void start(Stage primaryStage) {  
        Text fnum_lbl=new Text("First Number"); //Name label
        Text snum_lbl=new Text("Second Number"); //Password label
        Text ans_lbl=new Text("Answer"); //Password label
        Text op_lbl=new Text("Operations"); //Password label
        Text res_lbl=new Text("*****"); //Password label

        TextField fnum_tf=new TextField(); //User name text field
        TextField snum_tf=new TextField(); //User name text field

        Button sum_btn = new Button("Sum"); //Login Button
        Button Diff_btn = new Button("Difference"); //Login Button
        Button Ave_btn = new Button("Average"); //Login Button
        Button Dive_btn = new Button("Divide"); //Login Button
        Button sci_btn = new Button("Scientific Calculator"); //Exit Button
        Button close_btn = new Button("Exit"); //Exit Button

        GridPane gridPane = new GridPane();
        gridPane.setMinSize(800,400);
        gridPane.setVgap(20);
        gridPane.setHgap(20);
        gridPane.setAlignment(Pos.CENTER);



        gridPane.add(fnum_lbl, 1, 1);
        gridPane.add(fnum_tf, 2, 1);        
        gridPane.add(snum_lbl, 3, 1);
        gridPane.add(snum_tf, 4, 1);

        gridPane.add(ans_lbl, 1, 2);
        gridPane.add(res_lbl, 2, 2);


        gridPane.add(op_lbl, 1, 3);
        //gridPane.add(Diff_btn, 2, 3);
        //gridPane.add(Ave_btn, 3, 3);
        //gridPane.add(Dive_btn, 4, 3);
        HBox vbButtons = new HBox();


        vbButtons.setSpacing(10);
        vbButtons.setPadding(new Insets(0, 0, 0, 0));
        vbButtons.getChildren().addAll(sum_btn, Diff_btn, Ave_btn, Dive_btn);

        gridPane.add(vbButtons, 2, 3,2,1);
        gridPane.add(sci_btn,2,4);
        gridPane.add(close_btn,2,5);

        //Event Handling for the buttons
        sum_btn.setOnMouseClicked((new EventHandler<MouseEvent>() {
         public void handle(MouseEvent event) {
           String fnum = fnum_tf.getText();
           String snum = snum_tf.getText();

           Double fnumber = Double.parseDouble(fnum);
           Double snumber = Double.parseDouble(snum);

           Double sum = fnumber + snumber ;

           String result = Double.toString(sum);

           res_lbl.setText(result);

         }
        }));

        Diff_btn.setOnMouseClicked((new EventHandler<MouseEvent>() {
         public void handle(MouseEvent event) {


                if ((fnum_tf.getText() == null || fnum_tf.getText().trim().isEmpty()) || (snum_tf.getText() == null || snum_tf.getText().trim().isEmpty())) {
                   res_lbl.setText("Check your Inputs");
                }
                else
                {              
                   res_lbl.setText(Double.toString(Double.parseDouble(fnum_tf.getText()) - Double.parseDouble(snum_tf.getText())));  
                }            
            }
        }));

        fnum_tf.setOnKeyReleased((new EventHandler<KeyEvent>(){
            @Override
            public void handle(KeyEvent event) {
                String input = fnum_tf.getText();

                if (!input.matches("\\d{0,7}([\\.]\\d{0,4})?"))
                {
                    fnum_tf.setText("");
                }

            }
        }));

         snum_tf.setOnKeyReleased((new EventHandler<KeyEvent>(){
            @Override
            public void handle(KeyEvent event) {
                String input = snum_tf.getText();

                if (!input.matches("\\d{0,7}([\\.]\\d{0,4})?"))
                {
                    snum_tf.setText("");
                }

            }
        }));


        sci_btn.setOnMouseClicked((new EventHandler<MouseEvent>() {
        public void handle(MouseEvent event) {

             gui_three g3 = new gui_three();
             g3.start(gui_three.thirdGuiStage);

        }
     }));
       
        close_btn.setOnMouseClicked((new EventHandler<MouseEvent>() {
                     public void handle(MouseEvent event) {
                      Stage stage = (Stage) close_btn.getScene().getWindow();  
                      stage.close();            
                     }
                  }));

        primaryStage.setTitle("CALCULATOR");

        Scene my_scene=new Scene(gridPane); //This is our scene

        primaryStage.setScene(my_scene);        
        primaryStage.show();
    }
}

public class gui_three extends Application {
   
    static Stage thirdGuiStage = new Stage();
   
    @Override
           
    public void start(Stage primaryStage) {
   
    Text greetings_lbl=new Text("Hello there! I am the SCIENTIFIC CALCULATOR"); //Name label
    Button cl_btn = new Button("Close"); //CLOSE Button  

    GridPane griPane = new GridPane();
    griPane.setMinSize(400,200);
    griPane.setVgap(20);
    griPane.setHgap(20);
    griPane.setAlignment(Pos.CENTER);        
    griPane.add(greetings_lbl, 1, 1);    
    griPane.add(cl_btn, 2, 3);

    cl_btn.setOnMouseClicked((new EventHandler<MouseEvent>() {
     public void handle(MouseEvent event) {
      Stage stage = (Stage) cl_btn.getScene().getWindow();  
      stage.close();            
        }
      }));
   
    primaryStage.setTitle("SCIENTFIC CALCULATOR");        
    Scene scie_scene=new Scene(griPane); //This is our scene        
    primaryStage.setScene(scie_scene);        
    primaryStage.show
