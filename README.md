# Help-Dapper

#### Pacote para Asp.NET Core

```
dotnet add package Dapper --version 2.0.35
```

#### Configurar injeção em Startup

```
public Startup(IConfiguration configuration, IWebHostEnvironment env)
{
  Configuration = configuration;
}

public IConfiguration Configuration { get; }
```


#### Injeção de dependencia / Controller

```
private readonly IConfiguration _configuration;
public AgendaController(IConfiguration configuration)
{
    _configuration = configuration;    
}
```

#### Usando Dapper:

```
public string GetConnection()
{
    var connection = _configuration.GetSection("ConnectionStrings").GetSection("DefaultConnection").Value;
    return connection;
}

public IEnumerable<Product> ProductGetAll() 
{
    using (var _dapper = new SqlConnection(GetConnection()))
    {
       return _dapper.Query<Product>("SELECT * FROM PRODUCT");
    }            
}
```
