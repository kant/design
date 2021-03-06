# Supported Annotations 

Prism supports the following annotations in the metadata section of all Kubernetes standard and custom resources: 

1. prism.subkind: \<subkind value\>

   The prism.subkind annotation qualifies a Kubernetes resource kind.  For example, qualifying that a deployment is Liberty or Node.js. The subkind specification plays a role in action config map selection for a Kubernetes resource as it appears in the Prism Application and Component level views. 

   See [Action Config Maps](https://github.com/kappnav/design/blob/master/actions-config-maps.md) and [UI layout](https://github.com/kappnav/design/blob/master/UI-layout.md) for further details. 

   The \<subkind value\> must be a valid Kubernetes resource kind name. The subkind annotation is optional.  There is no default.  If not specified, the resource simply has no subkind. The following pre-defined subkinds are used by Prism: 

   1. Liberty
   1. Nodejs
   1. Swift 
   
   Note: the character set for subkind: 
   
   The prism.subkind value must consist of lower case alphanumeric characters or '-', start with an alphabetic character, and end with an alphanumeric character (e.g. 'my-name',  or 'abc-123', regex used for validation is '[a-z]([-a-z0-9]*[a-z0-9])?')
   
   
1. prism.platform : \<platform value\>

   The prism.platform annotation identifies the platform on which a Kubernetes resource is deployed. This information is used primarily to promote end user understanding while interacting with an application through the Prism UI. 
   
   The \<platform value\> must be a valid Kubernetes resource kind name.  The platform annotation is optional. The default is 'Kube'.   

   The following pre-defined platform values are used by Prism: 
   
   1. Kube
      
      Specifies the platform is a Kubernetes cluster. 

   1. WASCell

      Specifies the platform is a WebSphere Application Server Network Deployment cell. 

   1. VM 

      Specifies the platform is a virtual machine.  
      

1. prism.platform.name: <platform name value>

   The prism.platform.name annotation identifies the name of the platform on which a Kubernetes resource is deployed.  This information is used primarily to promote end user understanding while interacting with an application through the Prism UI.  
   
   The \<platform name value\> must be a valid Kubernetes resource name. There is no default value.  If platform name is not specified, the resource simply has not exposed the name of the platform on which it is deployed. 
   
 
