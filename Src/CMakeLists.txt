cmake_minimum_required(VERSION 3.18)

project("KeLi.HelloCMake" CSharp)

set(LIBS_PATH "../../Peroson/KeLi.Libs" CACHE PATH INTERNAL)

add_subdirectory("KeLi.HelloCMake.ConsoleApp")
add_subdirectory("KeLi.HelloCMake.WinFormApp")
add_subdirectory("KeLi.HelloCMake.WpfApp")
add_subdirectory("KeLi.HelloCMake.Business")
add_subdirectory("KeLi.HelloCMake.Utils")