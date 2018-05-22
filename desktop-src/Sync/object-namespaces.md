---
Description: 'An object namespace protects named objects from unauthorized access.'
ms.assetid: '6a84ec16-fa65-4cdd-861a-eccf5d0eee2b'
title: Object Namespaces
---

# Object Namespaces

An *object namespace* protects named objects from unauthorized access. Creating a private namespace enables applications and services to build a more secure environment.

A process can create a private namespace using the [**CreatePrivateNamespace**](createprivatenamespace.md) function. This function requires that you specify a *boundary* that defines how the objects in the namespace are to be isolated. The caller must be within the specified boundary for the create operation to succeed. To specify a boundary, use the [**CreateBoundaryDescriptor**](createboundarydescriptor.md) and [**AddSIDToBoundaryDescriptor**](addsidtoboundarydescriptor.md) functions.

The *lpAliasPrefix* parameter of [**CreatePrivateNamespace**](createprivatenamespace.md) serves as the name of the namespace. Each namespace is uniquely identified by its name and boundaries. The system supports multiple private namespaces with the same name, as long as they specify different boundaries.

Suppose that a process requests the creation of a namespace, NS1, that defines a boundary containing two elements: the administrator SID and the current session number. The namespace is created if the process is running under the Administrator account in the specified session. Another process can access this namespace using the [**OpenPrivateNamespace**](openprivatenamespace.md) function. Both the specified name and boundary must match if this process is to open the namespace created by the first process. Note that a process can open an existing namespace even if it is not within the boundary unless the creator restricted access to the namespace using the *lpPrivateNamespaceAttributes* parameter.

The objects that are created in this namespace have names that are of the form *prefix*\\*objectname*. The prefix is the namespace name specified by the *lpAliasPrefix* parameter of [**CreatePrivateNamespace**](createprivatenamespace.md). For example, to create an event object named MyEvent in the NS1 namespace, call the [**CreateEvent**](createevent.md) function with the *lpName* parameter set to NS1\\MyEvent.

The process that created the namespace can use the [**ClosePrivateNamespace**](closeprivatenamespace.md) function to close the handle to the namespace. The handle is also closed when the process that created the namespace terminates. After the namespace handle is closed, subsequent calls to [**OpenPrivateNamespace**](openprivatenamespace.md) fail, but all operations on objects in the namespace succeed.

## Related topics

<dl> <dt>

[Kernel Object Namespaces](termserv.kernel_object_namespaces)
</dt> </dl>

 

 


