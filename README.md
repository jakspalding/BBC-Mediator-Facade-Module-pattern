Structure diagram
-----------------
![Structure diagram](https://raw.github.com/middric/BBC-Mediator-Facade-Module-pattern/master/structure_diagram.png)

Component lifecycle
-------------------
![Component lifecycle](https://raw.github.com/middric/BBC-Mediator-Facade-Module-pattern/master/component_lifecycle.png)

    mediator:init
This method initializes the component mediator. The method should contain setup code that needs to be executed on component load. This function is only executed once, any code that must run whenever the component is activated should be in mediator:resume.

    mediator:stop
This method stops the mediator from executing any more code. Use this to effectivly turn the component off.

    mediator:resume
This method resumes the mediator after being stopped.

    supermediator:init
This method initializes the component mediator, attaches any config variables and sets up its child modules ready for execution.

    supermediator:addModules
This method adds modules to the mediator, it should be executed by the mediator:init method before calling this._super()

    supermediator:ready
This method executed the attached module constructors

    supermediator:stop
This method executes the attached module stop methods

    module:init
This method initializes the module. The method should contain setup code that needs to be executed on module load. This function is only executed once, any code that must run whenever the module is activated should be in module:resume.

    module:resume
This method resume the module after being stopped. This method is also executed automatically after the superfacade:init method. Calls to module methods that attach event bindings should be here alongside any setup code.

    module:stop
This method stops the module from executing. Calls to module methods that detach event bindings should be here alongside any cleanup code.

    superfacade:init
Currently this method only executes the module:resume method

    superfacade:resume
The method enables any Signals attached to the module

    superfacade:stop
This method disables any Signals attached to the module

Aims
----
*  Re-usable modules
    *  smallest units of 'real work' - i.e. carousel pagination
*  Decoupled module dependencies
*  Re-usable components
    *  groups of modules - i.e. carousel + pagination + filters
*  Per component config, per module config
*  Page level component mediator
*  Removal of pub/sub pattern in favour of direct method calls
    *  Components should not have ability to talk directly
    *  Contact between modules should be minimized by using a mediator
    *  Increases code robustness
    *  Decreases maintenance cost
*  Removal of MVC pattern in favour of Mediator/Facade/Module
    *  Allows for more modular codebase
    *  Conceptually similar to JavaScript
*  Minimized require dependencies
*  Minimized race condition gaps