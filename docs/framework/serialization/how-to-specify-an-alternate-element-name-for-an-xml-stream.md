---
title: "HOW TO：指定 XML 資料流的替代項目名稱 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "類別, 覆寫"
  - "覆寫類別"
  - "覆寫 XML 序列化"
  - "序列化, 覆寫"
  - "XML 序列化, 覆寫"
  - "XML 資料流, 指定其替代項目名稱"
ms.assetid: 5cc1c0b0-f94b-4525-9a41-88a582cd6668
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# HOW TO：指定 XML 資料流的替代項目名稱
[程式碼範例](#cpconoverridingserializationofclasseswithxmlattributeoverridesclassanchor1)  
  
 使用 [XmlSerializer](https://msdn.microsoft.com/en-us/library/system.xml.serialization.xmlserializer.aspx)，以相同類別集，可產生一個以上的 XML 資料流。當兩個不同的 XML Web 服務要求相同的基本資訊以及些微差異時，您也許會想這麼做。例如，試想有兩家處理書本訂單的 XML Web 服務，而且都需要 ISBN 號碼。一家服務使用標記 \<ISBN\>，另一家則是使用標記 \<BookID\>。您有名為 `Book` 的類別，其中包含名為 `ISBN` 的欄位。當 `Book` 類別的執行個體序列化時，它會根據預設使用成員名稱 \(ISBN\) 做為標記項目名稱。對於第一個 XML Web 服務，這正如預期。不過要想要傳送 XML 資料流至第二個 XML Web 服務，您必須覆寫序列化，讓標記的項目名稱為 `BookID`。  
  
### 以其他項目名稱建立 XML 資料流  
  
1.  建立 [XmlElementAttribute](frlrfSystemXmlSerializationXmlElementAttributeClassTopic) 類別的執行個體。  
  
2.  將 <xref:System.Xml.Serialization.XmlElementAttribute> 的 <xref:System.Xml.Serialization.XmlElementAttribute.ElementName%2A> 設為 "BookID"。  
  
3.  建立 [XmlAttributes](frlrfSystemXmlSerializationXmlAttributesClassTopic) 類別的執行個體。  
  
4.  將 **XmlElementAttribute** 物件加入至透過 <xref:System.Xml.Serialization.XmlAttributes> 之 <xref:System.Xml.Serialization.XmlAttributes.XmlElements%2A> 屬性存取的集合。  
  
5.  建立 [XmlAttributeOverrides](frlrfSystemXmlSerializationXmlAttributeOverridesClassTopic) 類別的執行個體。  
  
6.  將 **XmlAttributes** 加入至 <xref:System.Xml.Serialization.XmlAttributeOverrides>，傳遞要覆寫的物件型別及遭覆寫的成員名稱。  
  
7.  使用 **XmlAttributeOverrides** 建立 **XmlSerializer** 類別的執行個體。  
  
8.  建立 `Book` 類別的執行個體，將它序列化或還原序列化。  
  
## 範例  
  
```vb  
Public Class SerializeOverride()  
    ' Creates an XmlElementAttribute with the alternate name.  
    Dim myElementAttribute As XmlElementAttribute = _  
    New XmlElementAttribute()  
    myElementAttribute.ElementName = "BookID"  
    Dim myAttributes As XmlAttributes = New XmlAttributes()  
    myAttributes.XmlElements.Add(myElementAttribute)  
    Dim myOverrides As XmlAttributeOverrides = New XmlAttributeOverrides()  
    myOverrides.Add(typeof(Book), "ISBN", myAttributes)  
    Dim mySerializer As XmlSerializer = _  
    New XmlSerializer(GetType(Book), myOverrides)  
    Dim b As Book = New Book()  
    b.ISBN = "123456789"  
    ' Creates a StreamWriter to write the XML stream to.  
    Dim writer As StreamWriter = New StreamWriter("Book.xml")  
    mySerializer.Serialize(writer, b);  
End Class  
  
```  
  
```csharp  
public class SerializeOverride()  
{  
    // Creates an XmlElementAttribute with the alternate name.  
    XmlElementAttribute myElementAttribute = new XmlElementAttribute();  
    myElementAttribute.ElementName = "BookID";  
    XmlAttributes myAttributes = new XmlAttributes();  
    myAttributes.XmlElements.Add(myElementAttribute);  
    XmlAttributeOverrides myOverrides = new XmlAttributeOverrides();  
    myOverrides.Add(typeof(Book), "ISBN", myAttributes);  
    XmlSerializer mySerializer =   
    new XmlSerializer(typeof(Book), myOverrides)  
    Book b = new Book();  
    b.ISBN = "123456789"  
    // Creates a StreamWriter to write the XML stream to.  
    StreamWriter writer = new StreamWriter("Book.xml");  
    mySerializer.Serialize(writer, b);  
}  
```  
  
 XML 資料流可能類似下列所示。  
  
```  
<Book>  
    <BookID>123456789</BookID>  
</Book>  
```  
  
## 請參閱  
 [XML 和 SOAP 序列化](../../../docs/framework/serialization/xml-and-soap-serialization.md)   
 [XmlSerializer](https://msdn.microsoft.com/en-us/library/system.xml.serialization.xmlserializer.aspx)   
 [XmlElementAttribute](frlrfSystemXmlSerializationXmlElementAttributeClassTopic)   
 [XmlAttributes](frlrfSystemXmlSerializationXmlAttributesClassTopic)   
 [XmlAttributeOverrides](frlrfSystemXmlSerializationXmlAttributeOverridesClassTopic)   
 [HOW TO：序列化物件](../../../docs/framework/serialization/how-to-serialize-an-object.md)   
 [HOW TO：還原序列化物件](../../../docs/framework/serialization/how-to-deserialize-an-object.md)   
 [HOW TO：還原序列化物件](../../../docs/framework/serialization/how-to-deserialize-an-object.md)