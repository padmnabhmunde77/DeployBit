*****************
DeployBit
*****************
A New Door to Salesforce
--------------------------
DeployBit is Salesforce Metadata API based, Lightweight Python Environment to Smoothen and Support your Development and Deployment Processes.


Supported API Calls
--------------------------
- ``Login``
- ``Deploy``
- ``Check Deploy Status``
- ``Cancel Deploy``
- ``Retrieve``
- ``Check Retrieve Status``
- ``Describe Metadata``
- ``List Metadata``
- ``Query``
- ``Query More``
- ``Search``
- ``Apex Execute``
- ``Logout``

Examples
--------------------------

``1. DeployBitSalesforce Constructor - DeployBitSalesforce(username,password,security_token,session_id,api_version,environment)``

  DeployBitSalesforce constructor returns us the object to be used for salesforce connection, provided with below details.

- ``username`` - Username of the salesforce org  
- ``password`` - Password of the salesforce org  
- ``security_token`` - Security Token of the salesforce org  
- ``session_id`` - Session Id of the salesforce org  
- ``api_version`` - Api Version of the salesforce org  eg. ``45.0``, default value is ``50.0``
- ``environment`` - Environment of the salesforce org  eg. ``login`` for Production org and ``test`` for sandbox, default value is ``login``

For example:

.. code-block:: python

    from DeployBit import DeployBitSalesforce
    sf=DeployBitSalesforce('test@test.com','test123','tEstTesting123','aksdhjhasdas5d6asdhjasgdhasrd5a354sd678asd','45.0','test')
  
------


``2. Login - login()``

  This method will login to salesforce and will return login details object using details provided to DeployBitSalesforce constructor if credentials are correct. Login details result will have attributes such as - ``serverUrl`` , ``metadataServerUrl``

For example:

.. code-block:: python

    from DeployBit import DeployBitSalesforce
    sf=DeployBitSalesforce('test@test.com','test123','tEstTesting123',None,'45.0','test')
    sf.login()

------

``3. Deploy - deploy(zip_file_path,**deploy_options)``

 This method will deploy provided package ``.zip`` using given ``deploy options`` to org and will return deployment/validation details.
 
- ``zip_file_path`` - File path for .zip to be deployed
- ``checkOnly`` - Flag decides type of deployment eg. ``Deployment`` or ``Validation``
- ``testLevel`` - This attributes decides the level of the test execustion eg. ``RunSpecifiedTests`` , ``NoTestRun``   
- ``runTests`` - A list of Apex classes containing tests run after deployment when ``RunSpecifiedTests``
- ``ignoreWarnings`` - This setting indicates that a deployment succeeds even if there are warnings (true)
- ``allowMissingFiles`` - Specifies whether a deploy succeeds even if files that are specified in package.xml are not in the zip file.
- ``autoUpdatePackage`` - Specifies whether a deploy continues even if files present in the zip file are not specified in package.xml.
- ``performRetrieve`` - Specifies whether a deploy continues even if files present in the zip file are not specified in package.xml.
- ``purgeOnDelete`` - If true, the deleted components in the destructiveChanges.xml manifest file aren't stored in the Recycle Bin.
- ``rollbackOnError`` - Indicates whether any failure causes a complete rollback (true) or not (false).
- ``singlePackage`` - Declares that the zipFile or deployRoot parameter points to a directory structure with a single package, as opposed to a set of packages.


For example:

.. code-block:: python

    from DeployBit import DeployBitSalesforce
    sf=DeployBitSalesforce('test@test.com','test123','tEstTesting123','45.0','test')
    sf.login()
    deploy_result=sf.deploy("/Documents/Release/TestClassPackage.zip",checkOnly=True,singlePackage=True,testLevel='runspecifiedtests',runTests=['DummyClasstest'])

