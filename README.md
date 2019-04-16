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
                
                
                {
                    throw new InvalidPluginExecutionException("Cannot use this name");
                }
           }
        
    }
}
