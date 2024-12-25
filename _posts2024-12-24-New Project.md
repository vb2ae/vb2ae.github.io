# vb2ae.ServiceLocator.MSDependencyInjection


## What is the common service locator?

The Common Service Locator (CSL) library serves as a shared interface for service location, aimed at both application and framework developers. By providing an abstraction layer over IoC (Inversion of Control) containers and service locators, the CSL library allows applications to access these capabilities indirectly, without the need for hard references. This design ensures that third-party applications and frameworks can leverage IoC and service location features without being locked into a specific implementation. Ultimately, the goal is to promote flexibility and interoperability across various development ecosystems.

## What is vb2ae.ServiceLocator.MSDependencyInjection?

vb2ae.ServiceLocator.MSDependencyInjection is an implementation of the Common Service Locator (CSL) for the Microsoft.Extensions.DependencyInjection library. Currently, it uses version 9 of Microsoft.Extensions.DependencyInjection, enabling it to support all Keyed services effectively.


## How to register your services

The ConfigureServices method is where we are registering the Objects for dependency injection

        private IServiceProvider Build()
        {
            if (_built)
                throw new InvalidOperationException("Build can only be called once.");
            _built = true;

            _defaultBuilder.ConfigureServices((context, services) =>
            {
                services.AddSingleton<IService, ServiceImpl>();
                services.AddTransient<ICar, Ford>();
                services.AddTransient<ICar, Toyota>();
                services.AddTransient<ICar, Chevy>();
                services.AddKeyedTransient<IPet, Dog>("Dog");
                services.AddKeyedTransient<IPet, Cat>("Cat");
            });

            _services = _defaultBuilder.Build().Services;
            CommonServiceLocator.ServiceLocator.SetLocatorProvider(() => new vb2ae.ServiceLocator.MSDependencyInjection.MSDependencyInjectionServiceLocator(_services));
            return _services;
        }



The line of code below registers vb2ae.ServiceLocator.MSDependencyInjection with the CommonServiceLocator

    CommonServiceLocator.ServiceLocator.SetLocatorProvider(() => new vb2ae.ServiceLocator.MSDependencyInjection.MSDependencyInjectionServiceLocator(_services));
            return _services;


## How to Get classes stored in Dependency Injection with the CommonServiceLocator

# GetService 

            var serviceType = typeof(IService);
            var result = CommonServiceLocator.ServiceLocator.Current.GetService(serviceType);

This returns a ServiceImpl

# GetService< T >

            var result = CommonServiceLocator.ServiceLocator.Current.GetInstance<IService>();

This returns a ServiceImpl

# GetInstance(serviceType, key)

            var serviceType = typeof(IPet);
            var key = "Cat";
            var result = CommonServiceLocator.ServiceLocator.Current.GetInstance(serviceType, key);

This returns an instance of Cat

# GetInstance< T >(key)

            var key = "Dog";
            var result = CommonServiceLocator.ServiceLocator.Current.GetInstance<IPet>(key);

This returns an instance of Dog     

# GetInstance(serviceType)

            var serviceType = typeof(IService);
            var result = CommonServiceLocator.ServiceLocator.Current.GetInstance(serviceType);
            
This returns a ServiceImpl            

# GetInstance< T >

            var result = CommonServiceLocator.ServiceLocator.Current.GetInstance<IService>();

This returns a ServiceImpl   

# GetAllInstances(ServiceType)

            var result = CommonServiceLocator.ServiceLocator.Current.GetAllInstances(typeof(IPet));

Will return an IEnumerable<object> that contains a Cat and Dog

# GetAllInstances< T >

           var result = CommonServiceLocator.ServiceLocator.Current.GetAllInstances<ICar>()

Will return an IEnumerable<ICar> that contains a Ford, Chevy and Toyota

## Notes
Passing a null in as the key will return the first of the Type registered

            var serviceType = typeof(IPet);
            var result = CommonServiceLocator.ServiceLocator.Current.GetInstance(serviceType, null);

Will return the First IPet registered for DependencyInjection in this case an instance of the Dog class

All examples are based on what is registered in the How to register your services section
