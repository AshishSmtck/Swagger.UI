# Swagger.UI
Api testing of Swagger.UI code using several frameworks.


package testAPI;

import java.util.HashMap;
import org.testng.Assert;
import org.testng.annotations.Ignore;
import org.testng.annotations.Test;
import io.restassured.RestAssured;
import static io.restassured.RestAssured.*;
import io.restassured.response.Response;

public class GetApiId {
	@Test(priority=1)
	public void sendGetRequest() {
		RestAssured.baseURI="https://reqres.in/";
		RestAssured.basePath="api/users";
       Response response=RestAssured.given()
        .when().get()
        .then()
        .extract().response();
        
       String body=response.getBody().asString();
       System.out.println("Body of the code is "+body);
       
       int statusCode=response.getStatusCode();
       System.out.println("Status code is "+statusCode);
       }
       

       
	@Test(priority=2)
	public void sendPostLogin(){
		HashMap data=new HashMap();
		
			 data.put("username", "emma.wong@reqres.in"); 
			 data.put("email", "emma.wong@reqres.in");
			 data.put("password", "emma");
			
			 Response res=
			 given()
			 .contentType("application/json")
			 .body(data)
			 .when()
			 .post("https://reqres.in/api/login")
			 .then()
			.statusCode(200)
			.log().body().extract().response();
			 
			 String jsonString= res.asString();
			 Assert.assertEquals(jsonString.contains("user not found"),false);
		
	}
	@Test(priority=3)
	public void  sendPostRegister(){
		HashMap data=new HashMap(); 
		 data.put("email", "eve.holt@reqres.in");
		 data.put("password", "pistol");
		 Response response=RestAssured.given()
				 .body(data)
			        .when().post("https://reqres.in/api/register")
			        .then()
			        .extract().response();
			        
			       String body=response.getBody().asString();
			       System.out.println("Body of the code is "+body);
			       
			       int statusCode=response.getStatusCode();
			       System.out.println("Status code is "+statusCode);
			       }
	
	@Test(priority=4)
	public void putUserId(){
		HashMap data=new HashMap();
		 data.put("id", 20); 
		 Response response=RestAssured.given()
				 .body(data)
			        .when().put("https://reqres.in/api/users/2")
			        .then()
			 .statusCode(200)
			        .log().body()
			        .extract().response();
			        
		
		
	}
	@Test(priority=5)
	public  void deleteUserId() {
		HashMap data=new HashMap();
		
		 Response response=RestAssured.given()
				 .body(data)
			        .when().delete("https://reqres.in/api/users/2")
			        .then()
			        .log().body()
			        .extract().response();
		 
		             int statusCode=response.getStatusCode();
	                 System.out.println("Status code for delete user id is "+statusCode);			        
	}
	
		
}
