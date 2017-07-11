**Setting up Apache Derby**
---
The sample implimentation of this project makes use of Apache Derby as a stand alone database. In order to run this project you will need to set up Apache Derby on your local environment.

##### Download and Install Apache Derby

  - The instructions are provided at [Apache Derby: Quick Start](https://db.apache.org/derby/quick_start.html)
  - Once you install and start Derby, you will need to create a sample database that is used by this project.

##### Creating Sample Database

  - In `DERBY_HOME/bin` directory run `./ij`. ij is an interactive SQL scripting tool that comes with Derby.
  - On ij command prompt, run `connect 'jdbc:derby://localhost:1527/C:\Users\admin\temp\db;create=true';`. Here `C:\Users\admin\temp\db` is a path on my local machine, you should replace it as appropriate to your environment.
  - The above command will create a database instance.
  - Create tablse schema and sample records by running following at command line.
  
```
 CREATE TABLE CUSTOMERS (
    ID INTEGER NOT NULL GENERATED ALWAYS AS IDENTITY (START WITH 1, INCREMENT BY 1),`
    FIRST_NAME VARCHAR(255),
    LAST_NAME VARCHAR(255),
    BILLING_ADDRESS VARCHAR(255),
    SHIPPING_ADDRESS VARCHAR(255),
    IS_DELETED BOOLEAN,
	LAST_UPDATED TIMESTAMP
);

INSERT INTO CUSTOMERS (FIRST_NAME, LAST_NAME, BILLING_ADDRESS, SHIPPING_ADDRESS, IS_DELETED, LAST_UPDATED) VALUES ('David', 'J', 'Billing Address', 'Shipping Address', false, CURRENT_TIMESTAMP);
INSERT INTO CUSTOMERS (FIRST_NAME, LAST_NAME, BILLING_ADDRESS, SHIPPING_ADDRESS, IS_DELETED, LAST_UPDATED) VALUES ('Fibha', 'M', 'Billing Address', 'Shipping Address', false, CURRENT_TIMESTAMP);
INSERT INTO CUSTOMERS (FIRST_NAME, LAST_NAME, BILLING_ADDRESS, SHIPPING_ADDRESS, IS_DELETED, LAST_UPDATED) VALUES ('Marlon', 'V', 'Billing Address', 'Shipping Address', false, CURRENT_TIMESTAMP);
INSERT INTO CUSTOMERS (FIRST_NAME, LAST_NAME, BILLING_ADDRESS, SHIPPING_ADDRESS, IS_DELETED, LAST_UPDATED) VALUES ('John', 'Doe', 'Billing Address', 'Shipping Address', false, CURRENT_TIMESTAMP);
INSERT INTO CUSTOMERS (FIRST_NAME, LAST_NAME, BILLING_ADDRESS, SHIPPING_ADDRESS, IS_DELETED, LAST_UPDATED) VALUES ('Jane', 'Doe', 'Billing Address', 'Shipping Address', false, CURRENT_TIMESTAMP);
```

  - With above you have setup Derby database that the project uses. In order for the Mule application to connect to this database, a client driver is needed.

##### Add Dirby Client Driver to Build Path

  - Copy the derbyclient.jar (from the Derby installation zip you would have downloaded as a part of installing Derby) to your Mulesoft project.
  - Add this jar to the Build Path.
  
##### Update the Derby Configuration

  - Update the property `db.database = C:\\Users\\admin\\temp\\db` found in `sor-provider-DEV.properties` resource file to point to your database that you would have created as a part of first step above.
