---
title: "Query and edit an organization theme | MicrosoftDocs"
description: "Learn about defining and applying visual themes for an organization. This provides a supported way to apply an organization’s logo and color choices to the application. "
ms.custom: ""
ms.date: 10/31/2017
ms.reviewer: ""
ms.service: "crm-online"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "Dynamics 365 (online)"
ms.assetid: b9ad59fa-4778-4f79-9b24-94c320a33bde
caps.latest.revision: 20
author: "JimDaly"
ms.author: "jdaly"
manager: "amyla"
---
# Query and edit an organization theme

[!INCLUDE[](../../includes/cc_applies_to_update_9_0_0.md)]

You can define and apply visual themes for an organization. This provides a supported way to apply an organization’s logo and color choices to the application. You can create a custom theme for your application by making changes to the default colors and visual elements provided in the un-customized [!INCLUDE[pn_dynamics_crm](../../includes/pn-dynamics-crm.md)] Customer Engagement system. For example, you can create your personal product branding, add a company logo and provide entity-specific coloring. The theme colors are applied globally throughout the application, with the exception of some legacy areas.  
  
> [!NOTE]
> [!INCLUDE[cc_feature_included_with_2015_update_1_admins](../../includes/cc-feature-included-with-2015-update-1-admins.md)]  
  
 Theme customization is supported in this release only for the web application. The changes made for an organization's theme are not included in solutions exported from the organization. You can define multiple themes, but only one can be set and published as the default theme.  
  
 Video: [Theming in Microsoft Dynamics CRM](http://go.microsoft.com/fwlink/p/?LinkId=529568)  
  
<a name="BKMK_QueryTheme"></a>

## Query the current theme
 You may need to query the current theme using client-side code if you have a solution with HTML web resources which you want to adapt to theme choices made for an organization. You can use the following query with the Web API to retrieve that information.  

 **Request:** 

```http
GET <client_URL>/api/data/v8.0/themes?$filter=isdefaulttheme eq true&$select=defaultentitycolor,defaultcustomentitycolor,controlborder,controlshade,selectedlinkeffect,globallinkcolor,processcontrolcolor,headercolor,logotooltip,hoverlinkeffect,navbarshelfcolor,navbarbackgroundcolor
```

 **Response:**

```json
{  
    "@odata.context": "<client_URL>/api/data/v8.0/$metadata#themes(defaultentitycolor,defaultcustomentitycolor,controlborder,controlshade,selectedlinkeffect,globallinkcolor,processcontrolcolor,headercolor,logotooltip,hoverlinkeffect,navbarshelfcolor,navbarbackgroundcolor)",  
    "value": [  
        {  
            "defaultentitycolor": "#001CA5",  
            "defaultcustomentitycolor": "#006551",  
            "controlborder": "#CCCCCC",  
            "controlshade": "#F3F1F1",  
            "selectedlinkeffect": "#B1D6F0",  
            "globallinkcolor": "#1160B7",  
            "processcontrolcolor": "#D24726",  
            "headercolor": "#1160B7",  
            "logotooltip": "Microsoft CRM",  
            "hoverlinkeffect": "#D7EBF9",  
            "navbarshelfcolor": "#DFE2E8",  
            "navbarbackgroundcolor": "#002050",  
            "themeid": "f499443d-2082-4938-8842-e7ee62de9a23"  
        }  
    ]  
}  
```

 [!INCLUDE[proc_more_information](../../includes/proc-more-information.md)] [Query Data using the Web API](../webapi/query-data-web-api.md).
  
<a name="BKMK_EditAndPublish"></a>

## Edit and publish theme data

 A theme is created by using the customization tools in the UI, without requiring a developer to write code. Details about how to apply these customizations can be found in [Change the color scheme or add a logo to match your organization’s brand](https://technet.microsoft.com/library/21a166a0-d25e-4260-a1e4-2ddc528787c2.aspx).  

 Most theme data is stored within the Theme entity. Customized colors for specific entities is included in the <xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.EntityColor> property. This data is exported with the entity if the entity is included in a solution.

 The following table describes the `Theme` entity attributes that are valid for update and contain data that is applied by the theme:  

|Schema Name|Type|Value of default theme|Description|  
|-----------------|----------|----------------------------|-----------------|  
|ControlBorder|String|#CCCCCC|The color that controls will use for borders.|  
|ControlShade|String|#F3F1F1|The color for controls to use to indicate when you hover over items.|  
|DefaultCustomEntityColor|String|#006551|The default custom entity color if no color is assigned.|  
|DefaultEntityColor|String|#8B98AB|The default color for system entities if no color is assigned.|  
|GlobalLinkColor|String|#1160B7|The color for links, such as email addresses or lookups.|  
|HeaderColor|String|#1160B7|The color for header text, such as form tab labels.|  
|HoverLinkEffect|String|#D7EBF9|The color that commands or lists will use when you hover over the items.|  
|LogoId|String|null|The name of a web resource to use as a logo. Recommended dimensions are a height of 50 pixels and a maximum width of 400 pixels.|  
|LogoToolTip|String|Microsoft Dynamics 365|The text that will be used as the tooltip and alt text for the logo.|  
|Name|String|Dynamics 365 Default Theme|The name of the Theme entity.|  
|NavBarBackgroundColor|String|#002050|The primary navigation bar color.|  
|NavBarShelfColor|String|#DFE2E8|The secondary navigation bar color.|  
|ProcessControlColor|String|#0755BE|The primary color for process controls.|  
|SelectedLinkEffect|String|#B1D6F0|The color that commands or lists will use to indicate selected items.|  

 After you have applied changes, use the <xref:Microsoft.Crm.Sdk.Messages.PublishThemeRequest> message to make one of the theme records the current theme.  

<a name="BKMK_ExportingAndImportingThemes"></a>

## Exporting and importing themes

 Because themes aren’t included as part of a solution, if you want to transfer themes from one organization to another you can use the Configuration Migration tool to generate a schema, export the theme data, and import it into a different organization. For details about how to use this tool, see [Manage configuration data](https://technet.microsoft.com/library/dn647421.aspx).  

### See also

 [Theme Entity](../entities/theme.md)   
 [Developers guide to customization for Microsoft Dynamics 365](customize-applications.md)