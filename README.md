# th2 gRPC Data Provider library (1.3.0)

This library contains proto messages and `DataProvider` service with RPC methods that are used in [th2 data provider](https://github.com/th2-net/th2-rpt-data-provider "th2-rpt-data-provider"). See [data_provider.proto](src/main/proto/th2_grpc_data_provider/data_provider.proto "data_provider_template.proto") file for details. <br>
Tool generates code from `.proto` files and uploads built packages (`.proto` files and generated code) to specified repositories.

## How to maintain project
1. Make your changes.
2. Up version of Java package in `gradle.properties` file.
3. Up version of Python package in `package_info.json` file.
4. Commit everything.

## How to run project

### Java
If you wish to manually create and publish a package for Java, run the following command:
```
gradle --no-daemon clean build publish artifactoryPublish \
       -Purl=${URL} \ 
       -Puser=${USER} \
       -Ppassword=${PASSWORD}
```
`URL`, `USER` and `PASSWORD` are parameters for publishing.

### Python
If you wish to manually create and publish a package for Python:
1. Generate services with `Gradle`:
    ```
       gradle --no-daemon clean generateProto
    ```
   You can find the generated files by following path: `src/gen/main/services/python`
2. Generate code from `.proto` files and publish everything using `twine`:
    ```
    pip install -r requirements.txt
    pip install twine
    python setup.py generate
    python setup.py sdist
    twine upload --repository-url ${PYPI_REPOSITORY_URL} --username ${PYPI_USER} --password ${PYPI_PASSWORD} dist/*
    ```
   `PYPI_REPOSITORY_URL`, `PYPI_USER` and `PYPI_PASSWORD` are parameters for publishing.
