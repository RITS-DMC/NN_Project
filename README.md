
1. Clone the Node.js application from GitHub to your local system.
 
2. Understand the Project Structure
   
      This is a Node.js application with the following folder structure:
 
       db Folder – Handles PostgreSQL database operations:

           db-conn.js:  Establishes a virtual connection to a PostgreSQL database and creates the NN_SEQUENCE table.
 
           db-op.js:  Implements database operations such as create, read, update, and delete for number sequences.
 
       srv Folder – Server and business logic:

           server.js:  Creates API endpoints for all operations defined in the db folder.
 
           nn-gen-function.js:  The core logic for generating the Custom Next Number Pattern.
 
3. Build the mta.yaml file using your MTA build tool.
 
     ⚠️ Note:  If you encounter errors during the build, ensure the correct PostgreSQL version is specified in /pg-options.json:


       {

           "engine_version": "14"

        }
   

4. Deploy the generated .mtar archive to Cloud Foundry.
 
       ⚠️ Tip:  If a PostgreSQL service instance already exists, delete it before deploying. The deployment will automatically create a new one.
 
5. Get Deployment Details

       After deployment, copy the application's URL from Cloud Foundry.
 
6. Register API in Manage Service Registry

       Open the Manage Service Registry application.
 
       Go to the API tab and create a new entry with the following:
 
         Field	           Value

         Name	            nn_genseq_pg

         ID	              (Optional – generated automatically)

         Description	    (Optional)

         Group Path	       User-Defined

         Type	             HTTP

        Protocol	         REST

        Method	           POST

        URL/Path	        Your deployed app URL ending with / (e.g., https://your-app-url/)	

        Is Extension	    ✅ YES (This is very important)
 
         Click Create to finish registration.
 
7. Generate Custom Number Patterns

           Once the extension is registered, you can use it to generate custom next number patterns in various DMC flows:
 
           Batch Creation
 
           SFC Release
 
           SFC Serialize
 
8. Configure in SFC Serialize

         To use the extension in SFC Serialize:
 
         Open Manage Next Number app.
 
         Select SFC Serialize.
 
         In the Extension input field, click the Value Help icon.
 
         Choose the newly registered extension.
 
9. Generate the Custom Pattern in POD

        Open the Work Center POD.
 
        Select an SFC card.
 
        Click the Actions button in the top-right corner of the card.
 
        Choose SFC Serialize.
 
        Click Generate.
 
        You will now see your custom next number pattern displayed.

   if you cant see the next number pattern, check this line 26 under the nn-gen-function.js file at workCenterParam = extensionParameters["WORK_CENTER"];

   Change work center with any one of following:

            ORDER_NAME
            ORDER_TYPE
            PLANT
            MATERIAL_NAME
            SFC
            MATERIAL_VERSION
            PRIORITY

 
