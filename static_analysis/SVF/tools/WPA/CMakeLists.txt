
if(DEFINED IN_SOURCE_BUILD)
    set(LLVM_LINK_COMPONENTS BitWriter Core IPO IrReader InstCombine Instrumentation Target Linker Analysis ScalarOpts Support Svf Cudd)
    add_llvm_tool( wpa wpa.cpp )
    add_llvm_tool( spa spa.cpp )
else()
    llvm_map_components_to_libnames(llvm_libs bitwriter core ipo irreader instcombine instrumentation target linker analysis scalaropts support transformutils)
    add_executable( wpa wpa.cpp )
    add_executable( spa spa.cpp )

    target_link_libraries( wpa LLVMSvf LLVMCudd ${llvm_libs} )
    target_link_libraries( spa LLVMSvf LLVMCudd ${llvm_libs} )

    set_target_properties( wpa PROPERTIES
                           RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin )
    set_target_properties( spa PROPERTIES
                           RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin )
endif()


