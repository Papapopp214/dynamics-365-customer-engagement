---
title: "SiteMap schema (Developer Guide for Dynamics 365 Customer Engagement) | MicrosoftDocs"
description: "Dynamics 365 Customer Engagement displays commands in different ways depending on the entity and the client. In most places in the web application you will see a command bar instead of a ribbon."
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: pehecke

ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
applies_to: 
  - Dynamics 365 Customer Engagement (on-premises)
ms.assetid: 542dae08-58a7-4ed8-8a2d-58111633b7be
caps.latest.revision: 20
author: JimDaly
ms.author: jdaly
manager: amyla
search.audienceType: 
  - developer

---
# SiteMap schema

The following is the schema definition for the SiteMap portion of an import/export customization file. It is included from the [Customization Solutions File Schema](customization-solutions-file-schema.md). For more information, see [Package and Distribute Extensions with Microsoft Dynamics 365 Customer Engagement Solutions](../package-distribute-extensions-use-solutions.md).  
  
## SiteMap schema  

You can find this schema in the `Schemas\9.0.0.2090\SiteMap.xsd` folder when you download the Schemas zip file.

Download the [Schemas](https://download.microsoft.com/download/B/9/7/B97655A4-4E46-4E51-BA0A-C669106D563F/Schemas.zip).  
  
```xml  
<?xml version="1.0"?>  
<xs:schema attributeFormDefault="unqualified"  
           elementFormDefault="qualified"  
           xmlns:xs="https://www.w3.org/2001/XMLSchema">  
  <xs:include schemaLocation="SiteMapType.xsd" />  
  <xs:element name="SiteMap"  
              type="SiteMapType">  
    <xs:unique name="AreaIdMustBeUnique">  
      <xs:selector xpath="Area" />  
      <xs:field xpath="@Id" />  
    </xs:unique>  
  </xs:element>  
</xs:schema>  
```  
  
## SiteMap Type schema  

You can find this schema in the `Schemas\9.0.0.2090\SiteMapType.xsd` folder when you download the Schemas zip file.

Download the [Schemas](https://download.microsoft.com/download/B/9/7/B97655A4-4E46-4E51-BA0A-C669106D563F/Schemas.zip).  
  
```xml  
<?xml version="1.0"?>  
<xs:schema attributeFormDefault="unqualified"  
           elementFormDefault="qualified"  
           xmlns:xs="https://www.w3.org/2001/XMLSchema">  
  <xs:simpleType name="LCIDType_SiteMap">  
    <xs:restriction base="xs:decimal">  
      <xs:fractionDigits value="0"  
                         fixed="true" />  
      <xs:totalDigits value="4" />  
    </xs:restriction>  
  </xs:simpleType>  
  <xs:complexType name="TitlesType_SiteMap">  
    <xs:sequence>  
      <xs:element name="Title"  
                  minOccurs="1"  
                  maxOccurs="unbounded">  
        <xs:annotation>  
          <xs:appinfo>Title</xs:appinfo>  
          <xs:documentation>Specifies the text in a specific language to be displayed for the parent of the Titles element.</xs:documentation>  
        </xs:annotation>  
        <xs:complexType>  
          <xs:attribute name="LCID"  
                        type="LCIDType_SiteMap"  
                        use="required" >  
            <xs:annotation>  
              <xs:appinfo>Title.LCID</xs:appinfo>  
              <xs:documentation>A four digit Locale ID for the title.</xs:documentation>  
            </xs:annotation>  
          </xs:attribute>  
          <xs:attribute name="Title"  
                        type="xs:string"  
                        use="required" >  
            <xs:annotation>  
              <xs:appinfo>Title.Title</xs:appinfo>  
              <xs:documentation>Text to be displayed.</xs:documentation>  
            </xs:annotation>  
          </xs:attribute>  
  
        </xs:complexType>  
      </xs:element>  
    </xs:sequence>  
  
  </xs:complexType>  
  <xs:complexType name="DescriptionsType_SiteMap">  
    <xs:sequence>  
      <xs:element name="Description"  
                  minOccurs="1"  
                  maxOccurs="unbounded">  
        <xs:annotation>  
          <xs:appinfo>Description</xs:appinfo>  
          <xs:documentation>Provides a description in a specific language for the parent of the Descriptions element. Descriptions appear in Microsoft CRM for Microsoft Office Outlook and Microsoft CRM for Microsoft Office Outlook with Offline Access clients.</xs:documentation>  
        </xs:annotation>  
        <xs:complexType>  
          <xs:attribute name="LCID"  
                        type="LCIDType_SiteMap"  
                        use="required" >  
            <xs:annotation>  
              <xs:appinfo>Description.LCID</xs:appinfo>  
              <xs:documentation>A four digit Locale ID for the title.</xs:documentation>  
            </xs:annotation>  
          </xs:attribute>  
          <xs:attribute name="Description"  
                        type="xs:string"  
                        use="required" >  
            <xs:annotation>  
              <xs:appinfo>Description.Description</xs:appinfo>  
              <xs:documentation>Text to be displayed.</xs:documentation>  
            </xs:annotation>  
          </xs:attribute>  
  
        </xs:complexType>  
      </xs:element>  
    </xs:sequence>  
  
  </xs:complexType>  
  <xs:complexType name ="SiteMapType">  
    <xs:annotation>  
      <xs:appinfo>SiteMap</xs:appinfo>  
      <xs:documentation>Specifies the root node for the site map.</xs:documentation>  
    </xs:annotation>  
    <xs:sequence>  
      <xs:element name="Area"  
                  minOccurs="0"  
                  maxOccurs="unbounded">  
        <xs:annotation>  
          <xs:appinfo>Area</xs:appinfo>  
          <xs:documentation>Specifies an area that appears in the navigation pane.</xs:documentation>  
        </xs:annotation>  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="Titles"  
                        type="TitlesType_SiteMap"  
                        minOccurs="0"  
                        maxOccurs="1" >  
              <xs:annotation>  
                <xs:appinfo>Area/Titles</xs:appinfo>  
                <xs:documentation>Specifies a set of localizable Titles for the Area.</xs:documentation>  
              </xs:annotation>  
            </xs:element>  
            <xs:element name="Descriptions"  
                        type="DescriptionsType_SiteMap"  
                        minOccurs="0"  
                        maxOccurs="1" >  
              <xs:annotation>  
                <xs:appinfo>Area/Descriptions</xs:appinfo>  
                <xs:documentation>Specifies a set of localizable Descriptions for the Area.</xs:documentation>  
              </xs:annotation>  
            </xs:element>  
            <xs:element name="Group"  
                        minOccurs="0"  
                        maxOccurs="unbounded">  
              <xs:annotation>  
                <xs:appinfo>Group</xs:appinfo>  
                <xs:documentation>Specifies a group of subareas. Groups can be shown or hidden as defined by the area. Groups defined within the Workplace area can be marked as a user selectable profile. These profiles are available for users to select in their personal options.</xs:documentation>  
              </xs:annotation>  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="Titles"  
                              type="TitlesType_SiteMap"  
                              minOccurs="0"  
                              maxOccurs="1" >  
                    <xs:annotation>  
                      <xs:appinfo>Group/Titles</xs:appinfo>  
                      <xs:documentation>Specifies a set of localizable Titles for the Group.</xs:documentation>  
                    </xs:annotation>  
                  </xs:element>  
                  <xs:element name="Descriptions"  
                              type="DescriptionsType_SiteMap"  
                              minOccurs="0"  
                              maxOccurs="1" >  
                    <xs:annotation>  
                      <xs:appinfo>Group/Descriptions</xs:appinfo>  
                      <xs:documentation>Specifies a set of localizable Descriptions for the SubArea.</xs:documentation>  
                    </xs:annotation>  
                  </xs:element>  
                  <xs:element name="SubArea"  
                              minOccurs="0"  
                              maxOccurs="unbounded">  
                    <xs:annotation>  
                      <xs:appinfo>SubArea</xs:appinfo>  
                      <xs:documentation>Specifies a navigation option within an Area. Defines what will be displayed in the main pane of the application when selected.</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Titles"  
                                    type="TitlesType_SiteMap"  
                                    minOccurs="0"  
                                    maxOccurs="1" >  
                          <xs:annotation>  
                            <xs:appinfo>SubArea/Titles</xs:appinfo>  
                            <xs:documentation>Specifies a set of localizable Titles for the SubArea.</xs:documentation>  
                          </xs:annotation>  
                        </xs:element>  
                        <xs:element name="Descriptions"  
                                    type="DescriptionsType_SiteMap"  
                                    minOccurs="0"  
                                    maxOccurs="1" >  
                          <xs:annotation>  
                            <xs:appinfo>SubArea/Descriptions</xs:appinfo>  
                            <xs:documentation>Specifies a set of localizable Descriptions for the SubArea.</xs:documentation>  
                          </xs:annotation>  
                        </xs:element>  
                        <xs:element name="Privilege"  
                                    minOccurs="0"  
                                    maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:appinfo>Privilege</xs:appinfo>  
                            <xs:documentation>Controls whether a subarea is displayed based on privileges available in any security roles assigned to the user.</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:attribute name="Entity"  
                                          type="CRM_Entity_SiteMap" >  
                              <xs:annotation>  
                                <xs:appinfo>Privilege.Entity</xs:appinfo>  
                                <xs:documentation>Specifies the name of the entity to check privileges with.</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Privilege"  
                                          type="CRM_PrivilegeId_SiteMap" >  
                              <xs:annotation>  
                                <xs:appinfo>Privilege.Privilege</xs:appinfo>  
                                <xs:documentation>Specifies the privileges needed on the entity to display this subarea. </xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
  
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                      <xs:attribute name="Id"  
                                    type="CRM_Identifier_SiteMap"  
                                    use="required" >  
                        <xs:annotation>  
                          <xs:appinfo>SubArea.Id</xs:appinfo>  
                          <xs:documentation>A unique identifier for this SubArea element.</xs:documentation>  
                        </xs:annotation>  
                      </xs:attribute>  
                      <xs:attribute name="Title"  
                                    type="xs:string" >  
                        <xs:annotation>  
                          <xs:appinfo>SubArea.Title</xs:appinfo>  
                          <xs:documentation>Deprecated. Use the SubArea/Titles/Title element instead.</xs:documentation>  
                        </xs:annotation>  
                      </xs:attribute>  
                      <xs:attribute name="ResourceId"  
                                    type="xs:string" >  
                        <xs:annotation>  
                          <xs:appinfo>SubArea.ResourceId</xs:appinfo>  
                          <xs:documentation>For internal use only. Use the SubArea/Titles/Title element to set the text to display for this Group.</xs:documentation>  
                        </xs:annotation>  
                      </xs:attribute>  
                      <xs:attribute name="Icon"  
                                    type="xs:string" >  
                        <xs:annotation>  
                          <xs:appinfo>SubArea.Icon</xs:appinfo>  
                          <xs:documentation>Specifies a URL for an 18x18 pixel image to display for the SubArea.</xs:documentation>  
                        </xs:annotation>  
                      </xs:attribute>  
                      <xs:attribute name="OutlookShortcutIcon"  
                                    type="xs:string" >  
                        <xs:annotation>  
                          <xs:appinfo>SubArea.OutlookShortcutIcon</xs:appinfo>  
                          <xs:documentation>Specifies the icon to display in Microsoft CRM for Microsoft Office Outlook.</xs:documentation>  
                        </xs:annotation>  
                      </xs:attribute>  
                      <xs:attribute name="Url"  
                                    type="xs:string" >  
                        <xs:annotation>  
                          <xs:appinfo>SubArea.Url</xs:appinfo>  
                          <xs:documentation>Specifies a URL for a page to display in the main frame of the application when this subarea is selected.</xs:documentation>  
                        </xs:annotation>  
                      </xs:attribute>  
                      <xs:attribute name="PassParams"  
                                    type="xs:boolean"  
                                    use="optional" >  
                        <xs:annotation>  
                          <xs:appinfo>SubArea.PassParams</xs:appinfo>  
                          <xs:documentation>Specifies whether information about the organization and language context are passed to the URL.</xs:documentation>  
                        </xs:annotation>  
                      </xs:attribute>  
                      <xs:attribute name="Client"  
                                    type="CRM_Client_SiteMap" >  
                        <xs:annotation>  
                          <xs:appinfo>SubArea.Client</xs:appinfo>  
                          <xs:documentation>Specifies the client(s) that will display this SubArea.</xs:documentation>  
                        </xs:annotation>  
                      </xs:attribute>  
                      <xs:attribute name="AvailableOffline"  
                                    type="xs:boolean" >  
                        <xs:annotation>  
                          <xs:appinfo>SubArea.AvailableOffline</xs:appinfo>  
                          <xs:documentation>Controls whether SubArea is available when a user is working offline with the Microsoft CRM for Microsoft Office Outlook with Offline Access client.</xs:documentation>  
                        </xs:annotation>  
                      </xs:attribute>  
                      <xs:attribute name="CheckExtensionProperty"  
                                    type="xs:string" >  
                        <xs:annotation>  
                          <xs:appinfo>SubArea.CheckExtensionProperty</xs:appinfo>  
                          <xs:documentation>Controls whether SubArea is available based on the extension property.</xs:documentation>  
                        </xs:annotation>  
                      </xs:attribute>  
                      <xs:attribute name="Sku"  
                                    type="CRM_Sku_SiteMap" >  
                        <xs:annotation>  
                          <xs:appinfo>SubArea.Sku</xs:appinfo>  
                          <xs:documentation>Specifies the version(s) of Microsoft CRM that will display this SubArea.</xs:documentation>  
                        </xs:annotation>  
                      </xs:attribute>  
                      <xs:attribute name="License"  
                                    type="CRM_License_SiteMap" >  
                        <xs:annotation>  
                          <xs:appinfo>SubArea.License</xs:appinfo>  
                          <xs:documentation>Deprecated.</xs:documentation>  
                        </xs:annotation>  
                      </xs:attribute>  
                      <xs:attribute name="Entity"  
                                    type="CRM_Entity_SiteMap" >  
                        <xs:annotation>  
                          <xs:appinfo>SubArea.Entity</xs:appinfo>  
                          <xs:documentation>Specifies the name for the entity. If a Url is not specified, the default view of the specified entity will be displayed.</xs:documentation>  
                        </xs:annotation>  
                      </xs:attribute>  
                      <xs:attribute name="IntroducedVersion"  
                                    type="xs:string" >  
                        <xs:annotation>  
                          <xs:appinfo>SubArea.IntroducedVersion</xs:appinfo>  
                          <xs:documentation>IntroducedVersion of the SubArea.</xs:documentation>  
                        </xs:annotation>  
                      </xs:attribute>  
                      <xs:attribute name="Description"  
                                    type="xs:string" >  
                        <xs:annotation>  
                          <xs:appinfo>SubArea.Description</xs:appinfo>  
                          <xs:documentation>Deprecated. Use the SubArea/Descriptions/Description element instead.</xs:documentation>  
                        </xs:annotation>  
                      </xs:attribute>  
                      <xs:attribute name="DescriptionResourceId"  
                                    type="xs:string" >  
                        <xs:annotation>  
                          <xs:appinfo>SubArea.DescriptionResourceId</xs:appinfo>  
                          <xs:documentation>For internal use only. Use the SubArea/Descriptions/Description element instead.</xs:documentation>  
                        </xs:annotation>  
                      </xs:attribute>  
                      <xs:attribute name="ToolTipResourseId"  
                                    type="xs:string" >  
                        <xs:annotation>  
                          <xs:appinfo>SubArea.ToolTipResourseId</xs:appinfo>  
                          <xs:documentation>For internal use only. Use the SubArea/Descriptions/Description element instead.</xs:documentation>  
                        </xs:annotation>  
                      </xs:attribute>  
                      <xs:attribute name="GetStartedPanePath"  
                                    type="xs:string"  
                                    use="optional" >  
                        <xs:annotation>  
                          <xs:appinfo>SubArea.GetStartedPanePath</xs:appinfo>  
                          <xs:documentation>Specifies the path to the Get Started page for this subarea.</xs:documentation>  
                        </xs:annotation>  
                      </xs:attribute>  
                      <xs:attribute name="GetStartedPanePathOutlook"  
                                    type="xs:string"  
                                    use="optional" >  
                        <xs:annotation>  
                          <xs:appinfo>SubArea.GetStartedPanePathOutlook</xs:appinfo>  
                          <xs:documentation>Specifies the path to the Get Started page for this subarea when Microsoft CRM for Outlook is in use.</xs:documentation>  
                        </xs:annotation>  
                      </xs:attribute>  
                      <xs:attribute name="GetStartedPanePathAdmin"  
                                    type="xs:string"  
                                    use="optional" >  
                        <xs:annotation>  
                          <xs:appinfo>SubArea.GetStartedPanePathAdmin</xs:appinfo>  
                          <xs:documentation>Specifies the path to the Get Started page for this subarea if the user is logged in as an administrator. </xs:documentation>  
                        </xs:annotation>  
                      </xs:attribute>  
                      <xs:attribute name="DefaultDashboard"  
                                    type="xs:string"  
                                    use="optional" >  
                        <xs:annotation>  
                          <xs:appinfo>SubArea.DefaultDashboard</xs:appinfo>  
                          <xs:documentation>Specifies the GUID for default dashboard to be displayed for this subarea. </xs:documentation>  
                        </xs:annotation>  
                      </xs:attribute>  
                      <xs:attribute name="GetStartedPanePathAdminOutlook"  
                                    type="xs:string"  
                                    use="optional" >  
                        <xs:annotation>  
                          <xs:appinfo>SubArea.GetStartedPanePathAdminOutlook</xs:appinfo>  
                          <xs:documentation>Specifies the path to the Get Started page for this subarea if the user is logged in as an administrator and Microsoft CRM for Outlook is in use.</xs:documentation>  
                        </xs:annotation>  
                      </xs:attribute>  
  
                    </xs:complexType>  
                  </xs:element>  
                </xs:sequence>  
                <xs:attribute name="Id"  
                              type="CRM_Identifier_SiteMap"  
                              use="required" >  
                  <xs:annotation>  
                    <xs:appinfo>Group.Id</xs:appinfo>  
                    <xs:documentation>A unique identifier for this Group element.</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="Title"  
                              type="xs:string" >  
                  <xs:annotation>  
                    <xs:appinfo>Group.Title</xs:appinfo>  
                    <xs:documentation>Deprecated. Use the Group/Titles/Title element instead.</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="Icon"  
                              type="xs:string" >  
                  <xs:annotation>  
                    <xs:appinfo>Group.Icon</xs:appinfo>  
                    <xs:documentation>Unused. It is not possible to display an icon for a group.</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="Url"  
                              type="xs:string" >  
                  <xs:annotation>  
                    <xs:appinfo>Group.Url</xs:appinfo>  
                    <xs:documentation>  
                      Specifies the URL to render for the Outlook folder that represents the Group in Microsoft CRM for Outlook.  
                    </xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="ResourceId"  
                              type="xs:string" >  
                  <xs:annotation>  
                    <xs:appinfo>Group.ResourceId</xs:appinfo>  
                    <xs:documentation>For internal use only. Use the Group/Titles/Title element to set the text to display for this Group.</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="IsProfile"  
                              type="xs:boolean" >  
                  <xs:annotation>  
                    <xs:appinfo>Group.IsProfile</xs:appinfo>  
                    <xs:documentation>Controls whether this Group represents a user selectable Profile for the Workplace. This only applies for Groups within the Workplace Area.</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="License"  
                              type="CRM_License_SiteMap" >  
                  <xs:annotation>  
                    <xs:appinfo>Group.License</xs:appinfo>  
                    <xs:documentation>Deprecated.</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="IntroducedVersion"  
                              type="xs:string" >  
                  <xs:annotation>  
                    <xs:appinfo>Group.IntroducedVersion</xs:appinfo>  
                    <xs:documentation>IntroducedVersion of the Group.</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="Description"  
                              type="xs:string" >  
                  <xs:annotation>  
                    <xs:appinfo>Group.Description</xs:appinfo>  
                    <xs:documentation>Deprecated. Use the Group/Descriptions/Description element instead.</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="ToolTipResourseId"  
                              type="xs:string" >  
                  <xs:annotation>  
                    <xs:appinfo>Group.ToolTipResourseId</xs:appinfo>  
                    <xs:documentation>For internal use only. Use the Group/Descriptions/Description element instead.</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="DescriptionResourceId"  
                              type="xs:string" >  
                  <xs:annotation>  
                    <xs:appinfo>Group.DescriptionResourceId</xs:appinfo>  
                    <xs:documentation>For internal use only. Use the Group/Descriptions/Description element instead.</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
          <xs:attribute name="Id"  
                        type="CRM_Identifier_SiteMap"  
                        use="required" >  
            <xs:annotation>  
              <xs:appinfo>Area.Id</xs:appinfo>  
              <xs:documentation>A unique identifier for this Area element.</xs:documentation>  
            </xs:annotation>  
          </xs:attribute>  
          <xs:attribute name="Title"  
                        type="xs:string" >  
            <xs:annotation>  
              <xs:appinfo>Area.Title</xs:appinfo>  
              <xs:documentation>Deprecated. Use the Area/Titles/Title element instead.</xs:documentation>  
            </xs:annotation>  
          </xs:attribute>  
          <xs:attribute name="ResourceId"  
                        type="xs:string" >  
            <xs:annotation>  
              <xs:appinfo>Area.ResourceId</xs:appinfo>  
              <xs:documentation>For internal use only. Use the Area/Titles/Title element to set the text to display for this Area.</xs:documentation>  
            </xs:annotation>  
          </xs:attribute>  
          <xs:attribute name="Icon"  
                        type="xs:string" >  
            <xs:annotation>  
              <xs:appinfo>Area.Icon</xs:appinfo>  
              <xs:documentation>Specifies a URL for a 24x24 pixel image to display for the Area.</xs:documentation>  
            </xs:annotation>  
          </xs:attribute>  
          <xs:attribute name="Url"  
                        type="xs:string" >  
            <xs:annotation>  
              <xs:appinfo>Area.Url</xs:appinfo>  
              <xs:documentation>Specifies the Microsoft CRM for Outlook URL to render for the Outlook folder that represents the Area.</xs:documentation>  
            </xs:annotation>  
          </xs:attribute>  
          <xs:attribute name="ShowGroups"  
                        type="xs:boolean" >  
            <xs:annotation>  
              <xs:appinfo>Area.ShowGroups</xs:appinfo>  
              <xs:documentation>Control whether Groups of SubAreas within this Area are shown in the Navigation pane.</xs:documentation>  
            </xs:annotation>  
          </xs:attribute>  
          <xs:attribute name="License"  
                        type="CRM_License_SiteMap" >  
            <xs:annotation>  
              <xs:appinfo>Area.License</xs:appinfo>  
              <xs:documentation>Deprecated.</xs:documentation>  
            </xs:annotation>  
          </xs:attribute>  
          <xs:attribute name="IntroducedVersion"  
                        type="xs:string" >  
            <xs:annotation>  
              <xs:appinfo>Area.IntroducedVersion</xs:appinfo>  
              <xs:documentation>IntroducedVersion of the Area node.</xs:documentation>  
            </xs:annotation>  
          </xs:attribute>  
          <xs:attribute name="Description"  
                        type="xs:string" >  
            <xs:annotation>  
              <xs:appinfo>Area.Description</xs:appinfo>  
              <xs:documentation>Deprecated. Use the Area/Descriptions/Description element instead.</xs:documentation>  
            </xs:annotation>  
          </xs:attribute>  
          <xs:attribute name="ToolTipResourseId"  
                        type="xs:string" >  
            <xs:annotation>  
              <xs:appinfo>Area.ToolTipResourseId</xs:appinfo>  
              <xs:documentation>For internal use only. Use the Area/Descriptions/Description element instead.</xs:documentation>  
            </xs:annotation>  
          </xs:attribute>  
          <xs:attribute name="DescriptionResourceId"  
                        type="xs:string" >  
            <xs:annotation>  
              <xs:appinfo>Area.DescriptionResourceId</xs:appinfo>  
              <xs:documentation>For internal use only. Use the Area/Descriptions/Description element instead.</xs:documentation>  
            </xs:annotation>  
          </xs:attribute>  
  
        </xs:complexType>  
        <xs:unique name="GroupIdMustBeUnique">  
          <xs:selector xpath="Group" />  
          <xs:field xpath="@Id" />  
        </xs:unique>  
      </xs:element>  
    </xs:sequence>  
    <xs:attribute name="IntroducedVersion"  
                  type="xs:string" >  
      <xs:annotation>  
        <xs:appinfo>SiteMap.IntroducedVersion</xs:appinfo>  
        <xs:documentation>Specifies the IntroducedVersion of sitemap.</xs:documentation>  
      </xs:annotation>  
    </xs:attribute>  
    <xs:attribute name="Url"  
                  type="xs:string" >  
      <xs:annotation>  
        <xs:appinfo>SiteMap.Url</xs:appinfo>  
        <xs:documentation>Specifies the Microsoft CRM URL for Microsoft Office Outlook to load.</xs:documentation>  
      </xs:annotation>  
    </xs:attribute>  
  
  </xs:complexType>  
  <xs:simpleType name="CRM_Identifier_SiteMap">  
    <xs:annotation>  
      <xs:appinfo>CRM_Identifier_SiteMap</xs:appinfo>  
      <xs:documentation>Valid characters in this string are limited to: a-z, A-Z, 0-9, and the underscore(_) character. Spaces are not allowed.</xs:documentation>  
    </xs:annotation>  
    <xs:restriction base="xs:string">  
      <xs:pattern value="[a-zA-Z0-9_]+" />  
    </xs:restriction>  
  </xs:simpleType>  
  <xs:simpleType name="CRM_Client_SiteMap">  
    <xs:annotation>  
      <xs:appinfo>CRM_Client_SiteMap</xs:appinfo>  
      <xs:documentation>Valid values include:  'All'(default value),'Outlook', 'Web', 'OutlookWorkstationClient', and 'OutlookLaptopClient'. Multiple values can be used as long as they are separated by a comma and do not contain spaces. </xs:documentation>  
    </xs:annotation>  
    <xs:restriction base="xs:string">  
      <xs:pattern value="((Outlook|Web|All|OutlookWorkstationClient|OutlookLaptopClient),?)+" />  
    </xs:restriction>  
  </xs:simpleType>  
  <xs:simpleType name="CRM_Sku_SiteMap">  
    <xs:annotation>  
      <xs:appinfo>CRM_Sku_SiteMap</xs:appinfo>  
      <xs:documentation>Valid values include: 'All'(default value), 'OnPremise', 'Live', and 'SPLA'. Multiple values can be used as long as they are separated by a comma and do not contain spaces.</xs:documentation>  
    </xs:annotation>  
    <xs:restriction base="xs:string">  
      <xs:pattern value="((All|OnPremise|Live|SPLA),?)+" />  
    </xs:restriction>  
  </xs:simpleType>  
  <xs:simpleType name="CRM_License_SiteMap">  
    <xs:restriction base="xs:string" />  
  </xs:simpleType>  
  <xs:simpleType name="CRM_PrivilegeId_SiteMap">  
    <xs:annotation>  
      <xs:appinfo>CRM_PrivilegeId_SiteMap</xs:appinfo>  
      <xs:documentation>Valid values include: 'Read', 'Write', 'Append', 'AppendTo', 'Create', 'Delete', 'Share', 'Assign', 'All', 'AllowQuickCampaign', and 'UseInternetMarketing'. Multiple values can be used as long as they are separated by a comma and do not contain spaces.</xs:documentation>  
    </xs:annotation>  
    <xs:restriction base="xs:string">  
      <xs:pattern value="((Read|Write|Append|AppendTo|Create|Delete|Share|Assign|All|AllowQuickCampaign|CreateEntity|ImportCustomization|UseInternetMarketing),?)+" />  
    </xs:restriction>  
  </xs:simpleType>  
  <xs:simpleType name="CRM_Entity_SiteMap">  
    <xs:annotation>  
      <xs:appinfo>CRM_Entity_SiteMap</xs:appinfo>  
      <xs:documentation>Valid Entity has length greater than 1.</xs:documentation>  
    </xs:annotation>  
    <xs:restriction base="xs:string">  
      <xs:minLength value="1"/>  
    </xs:restriction>  
  </xs:simpleType>  
</xs:schema>  
  
```  
  
### See also  
 [Change Application Navigation using the SiteMap](../../developer/customize-dev/change-application-navigation-using-sitemap.md)   
 [Customization Solutions File Schema](customization-solutions-file-schema.md)   
 [Customization XML Reference](../customization-xml-reference.md)


[!INCLUDE[footer-include](../../../../includes/footer-banner.md)]