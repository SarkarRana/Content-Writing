# JSP Concepts
Java Server Pages allows to write java code in html

### LifeCycle
1. Jsp file is translated to Servlet
2. [[Servlet]] is loaded
3. Instantiation done
4. Initialize servlet using jspInit() method
5. Execute _jspService method
6. FInally jspDestroy method is called

### Declaration
`<%! Date date = new Date()>`
Declaration executes during jsp to servlet translation. It won't execute for each request. It creates a global variable in the generated servlet.

### Scriptlet
`<% date = new Date()>`
Scriptlet tag is used to pass any java code. It is executed each time a request is made.
The content of the scriptlet is placed in generated servlet's *_jspService()* method

### Expression
`<%=date>`
Expression prints in html. It prints to toString content

### Using Java Beans
It is better not to write java code in jsp and use java beans for business logic.
`<jsp:useBean id = "bean" class="package.class" scope="application">`
We can use EL to display `${bean.property}`
##### SetProperty
`<jsp:setProperty name="beanName" property="properyName" value="value">`
We can give * in property in case we want to set all fields of a form. We don't need a value attribute in that case
##### GetProperty
`<jsp:getProperty name="beanName" property="propertyName"`

### Invoking function using TLD
##### Steps
1. Create a Bean that implements Serializable and has the target method
2. Create a TLD file 
3. Add the function tag 
`<function>
<name>isPrimitive</name>
<function-class>org.javaeerecipes.chapter02.recipe02_05.ConditionalClass</function-class>
<function-signature>boolean isPrimitive(java.lang.String)</function-signature>
</function>`
4. Point to the tld in jsp file using taglib directive 
`<%@ taglib uri="/WEB-INF/tlds/functions.tld" prefix="fct">`
5. We can use this function using prefix
`<c:if test="${fct:isPrimitive(conditionalBean.typename)}" >`

### JSP Document
We can create a jsp document to adhere xml standard. It is easy for development and maintenance.
we can change jsp a little bit to make it a jsp document
`<jsp:directive`
`<jsp:include`
`<jsp:expression`
We can add EL using `${1+1==2}`
Few words are reserved for EL such as *eq,gt,ge,ne,lt,le* etc

### Implicit JSP Objects
1. session
2. request
3. response
4. out
5. page
6. pageContext
7. config
8. application
9. exception

### Creating a Custom Tag
1. First we have to create a class that implements *SimpleTagSupport* interface and implement *doTag()* method
2. We have to create custom tld file and specify the class name and attribute if applicable.

`
<tag>
	<name>signature</name>
	<tag-class>org.javaeerecipes.chapter02.recipe02_09.Signature</tag-class>
	<attribute>
		<name>authorName</name>
		<rtexprvalue>true</rtexprvalue>
		<required>false</required>
	</attribute>
</tag>
`
3. Now we can use this custom tld in jsp file using below syntax
	- For JSP documents `<xmlns:cust="custom"`
	- For normal JSP `<%@taglib uri="custom" prefix="cust"`
	- Call using `<cust:signature attribute="some_attribute"`

### Adding another jsp page
We can add content of another jsp page by using `<jsp:include>`. We can also pass any parameter if required.
`
<jsp:include page="page1.jsp">
	<jsp:param>some param</jsp:param>
</jsp:include>
`
### Looping
We can use JSTL to loop through a list of records using 
`<c:forEach items${bean.property} var="objectName">
	${objectName.name}
</c:forEach>
`

### Error handling
We can error page by adding page directive isErrorPage
`<%@page isErrorPage="true"%>`
We can have access to the error using
`pageContext.errorData`






