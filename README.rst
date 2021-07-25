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

  DeployBitSalesforce constructor returns us the object to be used for salesforce connection, when provided with below details.

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

  This method establishes connection to salesforce using details provided to DeployBitSalesforce constructor if credentials are correct and returns `LoginResult <https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_login_loginresult.htm#topic-title>`__.


For example:

.. code-block:: python

    from DeployBit import DeployBitSalesforce
    sf=DeployBitSalesforce('test@test.com','test123','tEstTesting123',None,'45.0','test')
    sf.login()

------

``3. Deploy - deploy(zip_file_path,**deploy_options)``

 This method deploys provided package ``.zip`` and returns deployment/validation status details using given `DeployOptions <https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/meta_deploy.htm>`__.
 
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
--------

``4. Check Deploy Status - check_deploy_status(deployment_id,include_details)``

 This method checks current deployment status using provided ``deployment_id``, ``include_details`` as ``True`` and returns deployment/validation details as given in `DeployResult <https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/meta_deployresult.htm>`__.
 

For example:

.. code-block:: python

    from DeployBit import DeployBitSalesforce
    sf=DeployBitSalesforce('test@test.com','test123','tEstTesting123','45.0','test')
    sf.login()
    deploy_result=sf.check_deploy_status('DeploymentId',include_details=True)

--------

``5. Cancel Deploy - cancel_deploy(deployment_id)``

 This method cancels ongoing deployment using provided ``deployment_id``.
 

For example:

.. code-block:: python

    from DeployBit import DeployBitSalesforce
    sf=DeployBitSalesforce('test@test.com','test123','tEstTesting123','45.0','test')
    sf.login()
    deploy_result=sf.cancel_deploy('DeploymentId')
----------

``6. Retrieve - retrieve(xml_file_path,single_package)``

 This method initiates retrieve request for all mentioned components in the package.xml path provided in ``xml_file_path`` and returns ``retrieve_id`` to be used to get package data. Package behaviour will be based on ``single_package`` flag.

For example:

.. code-block:: python

    from DeployBit import DeployBitSalesforce
    sf=DeployBitSalesforce('test@test.com','test123','tEstTesting123','45.0','test')
    sf.login()
    retrieve_result=sf.retrieve("/Documents/Release/download.xml",single_package=True)
 
----------

``7. Check Retrieve Status - check_retrieve_status(retrieve_id,include_zip)``

 This method returns initiated retrieve request status using provided ``retrieve_id`` and returns `RetrieveResult <https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/meta_retrieveresult.htm>`__ containing ``base64 zip string`` to be used for zip package generation if ``include_zip`` option is marked to ``True``.

For example:

.. code-block:: python

    from DeployBit import DeployBitSalesforce
    import base64,os
    sf=DeployBitSalesforce('test@test.com','test123','tEstTesting123','45.0','test')
    sf.login()
    retrieve_result=sf.check_retrieve_status('RetrieveId',include_zip=True)
    currentDirectory='/Documents/Release'
    with open(os.path.join(currentDirectory,'output_file.zip'), 'wb') as result:
            result.write(base64.b64decode(retrieve_result['zipFile']))
----------

``8. Describe Metadata - describe_metadata()``

 This method uses provided ``api_version`` in DeployBitSalesforce object and retrieves the metadata that describes your organization in `DescribeMetadataResult <https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/meta_describemeta_result.htm>`__.

For example:

.. code-block:: python

    from DeployBit import DeployBitSalesforce
    sf=DeployBitSalesforce('test@test.com','test123','tEstTesting123','45.0','test')
    sf.login()
    describe_result=sf.describe_metadata()
   
  

