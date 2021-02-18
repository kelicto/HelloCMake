cmake_minimum_required(VERSION 3.18)

project("KeLi.HelloCMake.WinFormApp" LANGUAGES CSharp)

# Includes CMake utilities for CSharp, for WinForm and WPF application support.
include(CSharpUtilities)

# Defines a variable to manage some resources.
set(RESOURCE_NAME
    "Data/001"
    "Data/002"
)

# Sets the build action of the custom resources.
set_property(SOURCE ${RESOURCE_NAME} PROPERTY VS_TOOL_OVERRIDE "Resource")

# Defines the executable, including any .cs files. 
# The .resx and other Properties files are optional here, but including them makes them visible in the VS solution for easy editing. 
add_executable(${PROJECT_NAME}
    App.config
    Properties/AssemblyInfo.cs
    Properties/Resources.resx
    Properties/Resources.Designer.cs
    Properties/Settings.settings
    Properties/Settings.Designer.cs
    
    Program.cs
    
    MainForm.cs
    MainForm.Designer.cs
    MainForm.resx
    
    ${RESOURCE_NAME}
)

# Sets resource file properties.
csharp_set_designer_cs_properties(
    Properties/AssemblyInfo.cs
    Properties/Resources.resx
    Properties/Resources.Designer.cs
    Properties/Settings.settings
    Properties/Settings.Designer.cs
)

# Sets the source file properties for Windows Forms.
csharp_set_windows_forms_properties(
    App.config
    
    Program.cs
    
    MainForm.cs
    MainForm.Designer.cs
    MainForm.resx
)

# Sets the .NET Framework version.
set_property(TARGET ${PROJECT_NAME} PROPERTY VS_DOTNET_TARGET_FRAMEWORK_VERSION "v4.5")

# Sets the root namespace.
set_property(TARGET ${PROJECT_NAME} PROPERTY VS_GLOBAL_ROOTNAMESPACE ${PROJECT_NAME})

# Sets the executable to be 32/64-bit.
set_property(TARGET ${PROJECT_NAME} PROPERTY WIN32_EXECUTABLE TRUE)

# Sets the C# language version (defaults to 3.0).
set(CMAKE_CSharp_FLAGS "/langversion:latest")

# Adds in the .NET reference libraries.
set_property(TARGET ${PROJECT_NAME} PROPERTY VS_DOTNET_REFERENCES
    "System"
    "System.Core"
    "System.Drawing"
    "System.Windows.Forms"
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