# Generic
Simplest MVC framework I could think of

HOW TO
======

Include Generic at the end of the page.
 
    DATA BINDINGS: 
    
        NB: adhoc models can be a global singleton, propertys can be a global model unto themselves in the absence of a model
        
        one-way <span model="person" find="10>id<100">{name}</span> (this becomes and iterable)
                      
        two-way <input model="person" find="name=*will*" value="{name}"> (this will throw an error?)
    
        two-way <span model="person" find="name=w%ill" contenteditable="true">{name}</span> ( this is problematic as it is an iterator)
         
        example: creates a new person model
            <form model="person">
                 <input name="name"><span class="{type}">{name}</span>  (class will always be empty in this example)
                 <button>save</button>
            </form>
                        
        example: edits an existing person model
            <form model="person">
                 <initial>
                    <input  type="text" name="name" find="name">
                 </inital>
                 <success>                          ( here we see a default custom form component )
                    <input type="text" name="name">
                 </success>
                 <error>
                    computer says no
                 </error>
            </form>
            
            
            
    TEMPLATING: ITERATE, FILTER, FIND...underscore methods
    

            iterate through the person collection
            <ul model="person">
                <li>location: {name}</li> <<---- This is the iterative template
            </ul
            
            
            iterate through a person object from the collection
            <ul model="person" select=param.id>
                <li>{key}: {value}</li>
            </ul>
            
            iteration can be forced
            <div model="person" select=param.id iterate>
                <p>{key}: {value}</p>
            </div>
                        
            iterate through a list property on the person model
            <ul model="person.listprop" select=param.id>
                <li>location: {name}</li>
            </ul
            
            filter the persons collection
            <ul model="person.list" select=param.id filter=param.query>
              <li>
                  <h2>location.name</h2>
                  <div>location.description</div>
              </li>
            </ul

                
                
    COMPONENTS: components are custion ui widgets.  they contain one or more top level elements which they recieve as a list of
    html elements.  it is upto the component to track state and wrap with the correct html
            <custom model="person">
                <div  name="template1">
                        this is template1: person.name
                </div>
                
                <div  name="template2">
                            this is template2: person.name
                </div>
            </custom>
    
    
    SCHEMAS object that provides validation to the models, schemas can contain simple validation rules & regexs or
    pointers to controllers
    
    there is also a PERSISTANCE object that contains the rules of when to push and pull the backend
    
    there is also an API abstraction that fits particular backends.  IE: any old web api or redis or a db
    