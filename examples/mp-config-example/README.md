# Microprofile Config
This is an example on how to use microprofile config in TomEE.

##### Run the application:

    mvn clean install tomee:run 

Within the application there is an three way to inject values using config

##### For the ConfigProperty with default value call:

    GET http://localhost:8080/mp-config-example/sample/defaultProperty
    
##### For the get property inject with ConfigProperty call:
    
     GET http://localhost:8080/mp-config-example/sample/injectedJavaVersion
     
##### For the get property from Config with getValue call:
    
     GET http://localhost:8080/mp-config-example/sample/javaVersion

##### Config Feature

MicroProfile Config is a solution to externalise configuration from microservices. 
Each individual property can be injected directly

     @Inject
     @ConfigProperty(name = "java.runtime.version")
     private String javaVersion;
     
You can also set a default value for it, case the config does not match the property in the context it will use the default value

    @Inject
    @ConfigProperty(name = "defaultProperty", defaultValue = "ALOHA")
    private String defaultProperty;
    
The config object can also be injected. Then use the getValue() method to retrieve the individual property.
    
    @Inject
    private Config config;
    
    @GET
    @Path("javaVersion")
    public String getJavaVersionPropertyFromSystemProperties() {
        return config.getValue("java.runtime.version", String.class);
    }