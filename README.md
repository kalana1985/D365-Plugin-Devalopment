# D365-Plugin-Devalopment
// Plugin is .Net Class Librery which impliment IPlugin Interface 
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.Xrm.Sdk;

namespace ItaintBoring
{
    public class ValidationPlugin : IPlugin
    {
       //IPLUGIN INTERFACE HAVE A EXECUTE METHORD WHICH TAKES A ONE PERAMETER//
       
        
            public void Execute(IServiceProvider serviceProvider)
            {
                IPluginExecutionContext context = (IPluginExecutionContext)
                    serviceProvider.GetService(typeof(IPluginExecutionContext));
                    
                    
         // SERVICePROVIDER PROVIDES THE CONTEXT AND YOU COULD GET CONTEXTUAL DETAILS USING CONTEXT 
         
            - context.InputParameters[“Target”]
             - context.PreEntityImages
              - context.PostEntityImages
             - context.MessageName
             - context.Stage
             
             //
             
             
                    
                Entity entity = (Entity)context.InputParameters["Target"];
                string name = (string)entity["ita_name"];
                if ("Test".Equals(name))
                
                // HERE WE GET'S THE "TARGET" FROM THE FROM CONTEXT.INPUTPARAMETER[];
                   *** THE "TARGET" HERE IS THE ENTITY OF WHICH THE ATTRIBUTE GET UPDATE
                       EG:- IF ACCOUNT ENTITY ATTRIBUTE GET UPDATES TARGET= ACCOUNT
                            IF CONTCAT ,,           ;;              TARGET=CONTCAT
                 //(IN ABOVE EXAMPLE WE ARE CHECKING A VALIDATION UP ON UPDATE AN ATTRIBUTE)
                 
                 ****IMP-- FOR for the “Create” and “Update” plugins, you will always have a “Target”, and it will be of “Entity” type.                      For the “Delete” plugins, you will also have a “Target”, but it will be of “EntityReference” type.
                
                
                {
                    throw new InvalidPluginExecutionException("Cannot use this name");
                }
           }
        
    }
}

*********Importent***************
We don’t always need an Organization Service in the plugins - we can get “Target” from the context, we can get the attributes, we can raise exceptions. We can write the whole validation plugin without ever having to create an Organization Service,


// WE USE SAME SERVICEPROVIDER PASSES BY THE EXECUTE METHORD TO get the OrganizationServices in order to access the OrganizationServices thet required to get the DB access in dynamics CRM

IOrganizationServiceFactory serviceFactory = (IOrganizationServiceFactory)serviceProvider.GetService(typeof(IOrganizationServiceFactory));
OrganizationService service = serviceFactory.CreateOrganizationService(context.UserId);

// create a in memory object for service.create 
Entity taskRecord=new Entity("task")// passing entity logical name

// Add singal line of text 

taskrecord.Attribute.Add("subject"//comes from task form attribute, "fallow up");
taskrecord.Attribute.Add("description", " type the discription");

// Optionset value
taskrecord.Attribute.Add("prioritcode" , new optionSetValue(1));

//Parent record or the entity

taskrecord.Attribute.Add("regardingobjectId", new EntityRefarance("contact",contact.Id);
                                                 // when working with the perent record or the 
                                                 // look up field you need to provide the Entityrefarance to provide the link to the 
                                                 // other entity record, passes the logical name of the entity and the guid.

Guid taskGuid=service.Create(taskRecord);


service.Retrive()// Requires a GUID of the record
Servive.RetriveMultipal()// Required Quirery

QueryExpression query=new QueryExpresson("contact")// pass the entity logical name

query.columset=new ColumSet(new string[]{"emailaddress1"});// use coulmset to specify the attribute , creates a new arrey 


// TO USE QUERRY YOU HAVE TO ADD, USING MICROSOFT.XRM.SDK.QUERY

YOU CAN RETRIVE DATA USING 
1 USING RETRIVE
2 QUERRY EXPRESSION 
3 QUEY BY ATTRIBUTE
4 FETCH XML
5 LINQ



