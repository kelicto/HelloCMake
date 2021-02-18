cmake_minimum_required(VERSION 3.18)

project("KeLi.HelloCMake.Utils" LANGUAGES CSharp)

# Includes CMake utilities for CSharp, for WinForm and WPF application support.
include(CSharpUtilities)

# Defines the library, including any .cs files. 
# The .resx and other Properties files are optional here, but including them makes them visible in the VS solution for easy editing. 
add_library(${PROJECT_NAME} SHARED
    Properties/AssemblyInfo.cs

    ProductUtil.cs
)

# Sets the .NET Framework version.
set_property(TARGET ${PROJECT_NAME} PROPERTY VS_DOTNET_TARGET_FRAMEWORK_VERSION "v4.5")

# Sets the root namespace.
set_property(TARGET ${PROJECT_NAME} PROPERTY VS_GLOBAL_ROOTNAMESPACE ${PROJECT_NAME})

# Sets the C# language version (defaults to 3.0).
set(CMAKE_CSharp_FLAGS "/langversion:latest")

# Adds in the .NET reference libraries.
set_property(TARGET ${PROJECT_NAME} PROPERTY VS_DOTNET_REFERENCES
    "System"
    "System.Core"
)

# If necessary, links in other library/DLL references, such as 3rd party libraries.
set_property(TARGET ${PROJECT_NAME} PROPERTY
    VS_DOTNET_REFERENCE_RevitAPI "${LIBS_PATH}/Revit.API.2016/RevitAPI.dll"
)
set_property(TARGET ${PROJECT_NAME} PROPERTY
    VS_DOTNET_REFERENCE_RevitAPIUI "${LIBS_PATH}/Revit.API.2016/RevitAPIUI.dll"
)

# If necessary, adds packages.
set_property(TARGET ${PROJECT_NAME} PROPERTY VS_PACKAGE_REFERENCES 
    "Newtonsoft.Json_12.0.3"
    
    "EPPlus_5.5.1"
    "Microsoft.IO.RecyclableMemoryStream_1.3.6"
    "System.ComponentModel.Annotations_4.7.0"
)
