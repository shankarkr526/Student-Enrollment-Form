# Student-Enrollment-Form
A simple HTML Web Application made with JavaScipt and JsonPowerDB for Student Enrollment Form.
<!DOCTYPE html>
<html>
    <head>
        <title>Login2Xplore's JsonPowerDB</title>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
        <script src="http://login2explore.com/jpdb/resources/js/0.0.3/jpdb-commons.js"></script>
         <script src="https://login2explore.com/jpdb/resources/js/0.0.3/JPDBObject.js"></script>

        <style type="text/css">
		th 
		{
			color: #000;
			font-size: 24px;
			font-weight: bold;
			text-align: left;
		}
		td	
		{
			color: #000;
		}
		body
   	 {
		background-color:#D3D3D3;
		color:white;
  		font-family:verdana;
	}
	</style>
    </head>
<body>

    <form id="myForm"  method="post">
<table width="700" border="0" align="center" cellpadding="0" cellspacing="5">
  <tr>
    <th width="25%" height="60">&nbsp;</th>
    <th><p>Student Enrollment Form</p></th>
    <th width="10%">&nbsp;</th>
  </tr>
  <tr>
    <td><strong>Roll No:</strong></td>
    <td><input id="rollno" name="rollno" type="text" size="35" required/></td>
    <td>&nbsp;</td>
  </tr>
  
  
  <tr>
    <td><strong>Name:</strong></td>
    <td><input id="name" name="name" type="text" size="35" required/></td>
    <td>&nbsp;</td>
  </tr>
   <tr>
    <td><strong>Class:</strong></td>
    <td><input id="class" name="Class" type="text" size="35" required/></td>
    <td>&nbsp;</td>
  </tr>
  
  <tr>
    <td><strong>DOB:</strong></td>
    <td><input id="dob" type="date" size="35" required/></td>
    <td>&nbsp;</td>
  </tr>
  <tr>
    <td><strong>Adress:</strong></td>
    <td><input id="adress" name="Adress" type="text" size="35" required/></td>
                </tr>
                <tr>
    <td><strong>Enrollment date:</strong></td>
    <td><input id="ed" type="date" size="35" required/></td>
    <td>&nbsp;</td>
  </tr>

</table>
<center>
<input type="reset" />
<input type="button" value="update" onclick="update();"/>
<input type="button" value="Save" onclick="registerCandidate();"/>
</center>
</form>
</body>

<script>
        function createPUTRequest(connToken, jsonObj, dbName, relName) {
            var putRequest = "{\n"
                    + "\"token\" : \""
                    + connToken
                    + "\","
                    + "\"dbName\": \""
                    + dbName
                    + "\",\n" + "\"cmd\" : \"PUT\",\n"
                    + "\"rel\" : \""
                    + relName + "\","
                    + "\"jsonStr\": \n"
                    + jsonObj
                    + "\n"
                    + "}";
            return putRequest;
        }
        function executeCommandAtGivenBaseUrl(reqString, dbBaseUrl, apiEndPointUrl) {
            var url = dbBaseUrl + apiEndPointUrl;
            var jsonObj;
            $.post(url, reqString, function (result) {
                jsonObj = JSON.parse(result);
            }).fail(function (result) {
                var dataJsonObj = result.responseText;
                jsonObj = JSON.parse(dataJsonObj);
            });
            return jsonObj;
        }

        function validateAndGetFormData() {
            var rollno = document.getElementById("rollno").value;
            var name = document.getElementById("name").value;
            var Class = document.getElementById("class").value;
            var dob = document.getElementById("dob").value;     
            var ed = document.getElementById("ed").value;
            var Adress = document.getElementById("adress").value;
           
            
            var jsonStrObj = {
                rollno: rollno,
                StudentName: name,
                Class: class,
                DOB: dob,
                EnrollmentDate: ed,
                Adress: adress,
            };
            return JSON.stringify(jsonStrObj);
        }
        

        function registerCandidate() {

            var jsonStr = validateAndGetFormData();
            if (jsonStr === "") {
                return;
            }
            var putReqStr = createPUTRequest("90938303|-31949273766497971|90952618",jsonStr, "SCHOOL-DB", "STUDENT-TABLE");
            alert(putReqStr);
            jQuery.ajaxSetup({async: false});
            var resultObj = executeCommandAtGivenBaseUrl(putReqStr,
                    "http://api.login2explore.com:5577", "/api/iml");
            jQuery.ajaxSetup({async: true});
            alert( "VALUES INSERTED "+ JSON.stringify(resultObj));
            document.getElementById("myForm").reset();
}

        
    </script>

</html>
