# XML
- XML = Extensible Markup Language.
- Goverened by **W3Org**.
- Final Version 1.0

- ### XML consits of 
	- ELEMENT
	- ATTRIBUTE

- ## 1. XML Element:
Element in an XML is written in angular braces for e.g. <beans>. In XML there are
two types of elements as follows
 - Start Element/Opening Tag: - Start element is the element which is written in <elementname> indicating the start of a block.
 - End Element/End Tag: - End element is the element which is written in x</elementname> indicating the end of a block. 
 
Type of element
 - Simple element
	  ```
		<simple-elem></sinple-elem>
	  ```
 - Compound element
		```
			<orderItems>
				<item>
					<itemCode>ic1001</itemCode>
					<quantity>35</quantity>
				</item>
			</orderItems>
		```

- ## 2. XML Attribute:
Attach supplementary information to element.


- ## XML Wellformess:
There are 3 rule:
1. Xml Must start with prolog 
		```
		<? xml version="1.0" encoding= "UTF-8"?>
		```
2. One and only one root element.
3. Every start Element must have a end element.

- ## XML Validity:
XML must be validate through DTD or XSD.

- ### [XML Example](po.xml)



# DTD:
- Document Type Documentation. Document which define the structure of an XML document.
- For writing DTD we need to write for simple and compound element.
- ### Synthax for Simple element
	```<!Element elementname (#PCDATA)>```
- ### Synthax for compount element:
	```
	    <!Element elementname(sub-elem1,sub-elem2(?/+/*),...)>
		where ? ->  occurence of sub-elem2 zero or 1 time.
			  + ->  occurence of sub-elem2 1 or many time.
			  * ->  occurence of sub-elem2 0 or many time.
	```
	[example of DTD for simple and compound element](po.dtd)
- Declaring Attribute for element:
	- To give option to attribute value or default value:``` <!ATTLIST elementname attributename (val1|val2) “default value”> ```
	- To have a fixed value of attribute : ```<!ATTLIST elementname attributename #FIXED “value”> ```
	- Presence of attribute is mandatory: ```<!ATTLIST elementname attributename #REQUIRED> ```
	- If attribute is not mandatory and not required value : ```<!ATTLIST elementname attributename #IMPLIED> ``` 
	- [Example of attribute DTD ](transport.dtd)
	- [Attribute DTD Example ](shipping.dtd)
- Drawbacks
	1. We dont have type of value. We only have #PCData i.e parsable character data.
	
	
	
# XSD
- XSD document is used for defining the structure of an XML document; it declares elements and the type of data that elements carry.
- XSD is also XML document. So it follow all XML wellformess rule.
- Synthax for writing simple element: 
	```<xs:element name=”elementname” type=”datatype”/> ```
- Synthax for writing coumpound element:
	```
		<xs:complexType name=”typeName”>
			<xs:sequence> or <xs:all>
				<xs:element name=”..” type=”..”/>
				<xs:element name=”..” type=”..”/>
				<xs:element name=”..” type=”..”/>
			</xs:sequence> or </xs:all>
		</xs:complexType> 
	```
- #### xs:sequence
	We write xs:sequence to indicate that all element must be in same oder. And it is written in complex tag. \n
	```
	<xs:element name=”person” type=”personType”/>
		<xs:complexType name=”personType”>
			<xs:sequence>
				 <xs:element name=”name” type=”xs:string”/>
				 <xs:element name="age" type=”xs:int”/>
			</xs:sequence>
	</xs:complexType> 
	```
	[EXAMPLE OF xs:sequence](Xsd/book.xsd)
- #### xs:all
	We write xs:all to indicate that all element must be there but not in same oder.
	```
	<xs:element name=”person” type=”personType”/>
		<xs:complexType name=”personType”>
			<xs:all>
				 <xs:element name=”name” type=”xs:string”/>
				 <xs:element name="age" type=”xs:int”/>
			</xs:all>
	</xs:complexType> 
	```
- #### Imposing restriction on simple Type:
	```
		<xs:simpleType name="phoneType">
			<xs:restriction base=”xs:int”>
				<xs:totalDigits value=”10”/>
			</xs:restriction>
		</xs:simpleType> 
	```
- #### xs:choice:
	If we want user to have choice in writing element.
	```
		<xs:choice>			
			<xs:element name="savings-account" type="savings-account-type"/>
			<xs:element name="corporate-account" type="corporate-account-type"/>
		</xs:choice>
	```
	- [Example of xs:choice](Xsd/accounts.xsd)
	- [Example of xs:choice where user have to write at least one using minoccur and maxocuur attribute](Xsd/gas-station.xsd)
- #### Extending the complex type:
	We can declare own type and we can also extend our type by mean of inheritance
	```
		<xs:complexType name=”USShippingAddressType”>
			<xs:complexContent>
				<xs:extension base=”shippingAddressType”>
					<xs:sequence>
						<xs:element name=”county” type=”xs:int”/>
					</xs:sequence>
				</xs:extension>
			</xs:complexContent>
		</xs:complexType>
	```
	- [Example of comple type extending](Xsd/travel-agency.xsd)
	- [Example of comple type and simple type extending](Xsd/medical-policy.xsd)
	
# XSD TArgetNameSpace
	When we create element and complex type and if elementFormname is qualified then we have to bind element with the namespace. To declare a namespace in XSD we need to use targetNameSpace attribute at the Schema level followed by targetnamespace
	```
		<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:eps="http://ebay.in/products/sales" targetNamespace="http://ebay.in/products/sales" elementFormDefault="qualified">
			<xs:element name="purchaseOrder" type="eps:purchaseOrderType"/>
				<xs:complexType name="purchaseOrderType">
					<xs:sequence>
						<xs:element name="orderItems" type="eps:orderItemsType"/>
						<xs:element name="shippingAddress" type="eps:shippingAddressType"/>
					</xs:sequence>
				</xs:complexType>
			</xs:element>
		</xs:schema>
	```
	- [Example of Target Namespace](Xsd\Namespaces\po.xsd)
	- [Example of Target Namespace where we have the bus ticket from xml and have 2 implementation and then redbus is using one of them](Xsd\Namespaces\redbus-ticket.xsd)
		- [Implementation of bus 1 ](Xsd\Namespaces\kesineni-ticket.xsd)
		- [Implementation of bus 2 ](Xsd\Namespaces\kaleswari-ticket.xsd)
# Import and Include
- 
