cmake_minimum_required(VERSION 3.18)

project("KeLi.HelloCMake.WpfApp" LANGUAGES CSharp)

# Include CMake utilities for CSharp, for WinForm and WPF application support.
include(CSharpUtilities)

# Defines the executable, including any .cs files. 
# The .resx and other Properties files are optional here, but including them makes them visible in the VS solution for easy editing. 
add_executable(${PROJECT_NAME}
    App.config
    
    Properties/AssemblyInfo.cs
    Properties/Resources.resx
    Properties/Resources.Designer.cs
    Properties/Settings.settings
    Properties/Settings.Designer.cs

    App.xaml
    App.xaml.cs
    
    MainWnd.xaml
    MainWnd.xaml.cs
)

# Sets resource file properties.
csharp_set_designer_cs_properties(
    Properties/AssemblyInfo.cs
    Properties/Resources.resx
    Properties/Resources.Designer.cs
    Properties/Settings.settings
    Properties/Settings.Designer.cs
)

# Sets the source file properties for WPF.
csharp_set_xaml_cs_properties(
    App.config

    App.xaml
    App.xaml.cs
    
    MainWnd.xaml
    MainWnd.xaml.cs
)

# Sets the xaml as ApplicationDefinition for WPF.
set_property(SOURCE App.xaml PROPERTY VS_XAML_TYPE "ApplicationDefinition")

# Sets the .NET Framework version.
set_property(TARGET ${PROJECT_NAME} PROPERTY VS_DOTNET_TARGET_FRAMEWORK_VERSION "v4.5")

# Sets the .NET Framework version.
set_property(TARGET ${PROJECT_NAME} PROPERTY VS_GLOBAL_ROOTNAMESPACE ${PROJECT_NAME})

# Sets the executable to be 32-bit.
set_property(TARGET ${PROJECT_NAME} PROPERTY WIN32_EXECUTABLE TRUE)

# Sets the C# language version (defaults to 3.0).
set(CMAKE_CSharp_FLAGS "/langversion:latest")

# Adds in the .NET reference libraries.
set_property(TARGET ${PROJECT_NAME} PROPERTY VS_DOTNET_REFERENCES
    "PresentationCore"
    "PresentationFramework"
    "System"
    "System.Core"
    "System.Xaml"
    "System.Xml"
    "WindowsBase"
)

# If necessary, links in other library dependencies that were built locally in this source tree.
target_link_libraries(${PROJECT_NAME}
    "KeLi.HelloCMake.Business"
    "KeLi.HelloCMake.Utils"
)

# If necessary, links in other library/DLL references, such as 3rd party libraries.
set_property(TARGET ${PROJECT_NAME} PROPERTY
    VS_DOTNET_REFERENCE_RevitAPI "${LIBS_PATH}/Revit.API.2016/RevitAPI.dll"
)
set_property(TARGET ${PROJECT_NAME} PROPERTY
    VS_DOTNET_REFERENCE_RevitAPIUI "${LIBS_PATH}/Revit.API.2016/RevitAPIUI.dll"
)