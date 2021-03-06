# Application Navigator for Kubernetes

![kappnav](https://github.com/kappnav/design/blob/master/images/prism.png)

{k}AppNav is a tool that extends the Kubernetes Console to provide display, inspection, understanding, and navigation through the deployed resources that comprise an application.

> Kubernetes is an open-source system for automating deployment, scaling, and management of containerized applications.

The above description, from the [Kubernetes homepage](https://kubernetes.io/), is centered on containerized _applications_. Yet, the Kubernetes metadata, objects, and visualizations (e.g., within Dashboard) are focused on container infrastructure rather than the applications themselves.

The Application CRD ([Custom Resource Definition](https://kubernetes.io/docs/concepts/api-extension/custom-resources/#customresourcedefinitions)) in the [Kubernetes Application](https://github.com/kubernetes-sigs/application) project aims to change that in a way that's interoperable between many supporting tools.

In Cloud Native application architectures, typically multiple microservices, plus some number of 'web apps', mobile front-ends, data bases, etc - taken together - comprise a (big "A") application in the eyes of an application architect.  

For an application deployed to Kubernetes, the Application CRD provides the basis for organizing the resources that comprise a big "A" application.  

For big "A" applications deployed across Kubernetes and non-Kubernetes environments - think WAS transformation - the non-Kubernetes assets _can_ be represented _in_ Kubernetes using CRDs. 

## Big Picture 

The following diagram depicts a big "A" application comprised of two Kubernetes deployments and a WAS ND (Java EE) application.  Assuming use of a "WAS ND App" CRD, an Application CRD can be used to define an Application (big "A") that comprises all three resources: 

![big picture](https://github.com/kappnav/design/blob/master/images/big-picture.png)

{k}AppNav provides visualization of all defined Applications, offering drill down into their respective comprised 'components'.  Each component is a Kubernetes resource.  Each Kubernetes resource has a 'Kind' - e.g. Deployment, Service, WAS-ND-App (a CRD), etc.  {k}AppNav offers configurable action menu items by Kind.  These menu items provide URLs that enable the user to navigate to other tools in context - e.g. the log, monitor, trace, configuration page (or tool) for the currently selected component. 

Taken together, all this provides a way to define, visualize, and navigate Cloud Native Applications, yielding a superior user experience for applications, that dramatically surpasses the infrastructure view offered by the ICP console itself. 

## Screen Shots

![applications](https://github.com/kappnav/design/blob/master/images/screen-shot-applications.png)

![components](https://github.com/kappnav/design/blob/master/images/screen-shot-components.png)
