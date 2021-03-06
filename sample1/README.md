# Sample1
The [soapui project](https://github.com/nmrao/soapui-projects/blob/master/sample1/checknumber-soapui-project.xml) that is present in [this directory](https://github.com/nmrao/soapui-projects/tree/master/sample1) address the following:

## Problem Description:

_Many times, the same question from different new users of `SoapUI` is noticed asking as below:_

There is a test case with _multiple steps_ and each step represents different operation either from the same service or from different service. The common problem is that **how to retrieve certain value from first step's response and pass that value to input to other test step** of same test case. Of course, it is not limited to either same test case or test suite as such though. 

## How to use this soapUI project:

Import this _soapui project_ into your SoapUI software. This will domonstrate the solution addressing the above mentioned problem by using mock service. 

### You would see the following artifcats in the project:
- checkNumberSOAP [this is a service interface]
- TestSuite1 [this is a test suite using the existing service operations]
- checkNumberSOAP MockService [this is a mock service which enables users to test]

### How to test:
<pre>
1. Start `checkNumberSOAP MockService` using right click.
2. Open the `TestSuite 1`, then `CheckIfNumberIsEvenOrOdd` test case.
3. Just, run the test case and you should find it execute successfully.
</pre>

## Into the details

### Service : _checkNumberSOAP_
This service contains below two _operations_:
<pre>
1. generateNumber - This does not require any input parameters. It will just return an Integers in the response.
2. isNumberEven - This has an input parameter, pass any Integer and user will recieve a response saying whether<br>                 that is an even or an odd numer.
</pre>
### Test Case : _CheckIfNumberIsEvenOrOdd_

>Note that this test case sample is using **Property Transfer** approach.

The test case contains the following 3 steps.
<pre>
1. GenerateNumber of soap request test type, this is using `generateNumber` operation.
2. Property Transfer
3. IsNumberEven of soap request test type, this is using `isNumberEven` operation.
</pre>
**Brief explanation on how the above is working**
If you notice, the first step does not have any inputs. Just it is getting a number from its service. 
**Property Transfer** step is retrieving the required value from its previous step i.e., `GenerateNumber` step and storing it as test case level custom property called `NUMBER`.
`NUMBER` property is being used in 3rd step's request as input and finally calling its service to check if the number is `odd or even`.<br>Also there are `assertions` defined to test steps if the ouput is desired or not.

### Test Case : _CheckIfNumberIsEvenOrOdd_Using_ScriptAssertion_

>Note that this test case sample is using **Script Assertion** approach to check if the previous step response has the value and store it in test case custom property. Have a look at assertion call `Store the number if valid response` for the first step. Having said that, it does not need any additional steps like `Property Transfer` used in 1st test case.

The test case contains the following 2 steps.
<pre>
1. GenerateNumber of soap request test type, this is using `generateNumber` operation.
2. IsNumberEven of soap request test type, this is using `isNumberEven` operation.
</pre>


I believe that this example is handy for to start with and improve upon it and apply to your projects. Good luck.

>Note: You may need to make the `change in the endpoint` for the test steps (SOAP Request Type) **replacing localhost with \<your hostname\> in case if it did not work when you start the mock service**.
