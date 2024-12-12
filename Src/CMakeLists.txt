set(PR_SOURCE ${SRC_DIR}/PoissonRecon.cpp)
set(PRC_SOURCE ${SRC_DIR}/PoissonReconClient.cpp)
set(PRS_SOURCE ${SRC_DIR}/PoissonReconServer.cpp)
set(SR_SOURCE ${SRC_DIR}/SSDRecon.cpp)
set(PI_SOURCE ${SRC_DIR}/PointInterpolant.cpp)
set(ST_SOURCE ${SRC_DIR}/SurfaceTrimmer.cpp)
set(EH_SOURCE ${SRC_DIR}/EDTInHeat.cpp)
set(IS_SOURCE ${SRC_DIR}/ImageStitching.cpp)
set(AV_SOURCE ${SRC_DIR}/AdaptiveTreeVisualization.cpp)
set(CP_SOURCE ${SRC_DIR}/ChunkPLY.cpp)
set(RE_SOURCE ${SRC_DIR}/Reconstruction.example.cpp)
set(PTD_SOURCE ${SRC_DIR}/PointsToDisks.cpp)

add_executable(PoissonRecon ${PR_SOURCE})
target_include_directories(PoissonRecon PRIVATE 
    ${CMAKE_SOURCE_DIR}
)
target_link_libraries(PoissonRecon PRIVATE 
    ${PNG_LIBRARIES} 
    Boost::system
)

add_executable(PoissonReconClient ${PRC_SOURCE})
target_include_directories(PoissonReconClient PRIVATE ${CMAKE_SOURCE_DIR})
target_link_libraries(PoissonReconClient PRIVATE Boost::system)

add_executable(PoissonReconServer ${PRS_SOURCE})
target_include_directories(PoissonReconServer PRIVATE ${CMAKE_SOURCE_DIR})
target_link_libraries(PoissonReconServer PRIVATE Boost::system)

add_executable(SSDRecon ${SR_SOURCE})
target_include_directories(SSDRecon PRIVATE ${CMAKE_SOURCE_DIR})
target_link_libraries(SSDRecon PRIVATE ${PNG_LIBRARIES})

add_executable(PointInterpolant ${PI_SOURCE})
target_include_directories(PointInterpolant PRIVATE ${CMAKE_SOURCE_DIR})
target_link_libraries(PointInterpolant PRIVATE ${PNG_LIBRARIES})

add_executable(SurfaceTrimmer ${ST_SOURCE})
target_include_directories(SurfaceTrimmer PRIVATE ${CMAKE_SOURCE_DIR})

add_executable(EDTInHeat ${EH_SOURCE})
target_include_directories(EDTInHeat PRIVATE ${CMAKE_SOURCE_DIR})

add_executable(ImageStitching ${IS_SOURCE})
target_include_directories(ImageStitching PRIVATE ${CMAKE_SOURCE_DIR})
target_link_libraries(ImageStitching PRIVATE ${PNG_LIBRARIES})

add_executable(AdaptiveTreeVisualization ${AV_SOURCE})
target_include_directories(AdaptiveTreeVisualization PRIVATE ${CMAKE_SOURCE_DIR})
target_link_libraries(AdaptiveTreeVisualization PRIVATE ${PNG_LIBRARIES})

add_executable(ChunkPLY ${CP_SOURCE})
target_include_directories(ChunkPLY PRIVATE ${CMAKE_SOURCE_DIR})
target_link_libraries(ChunkPLY PRIVATE ${PNG_LIBRARIES})

add_executable(ReconstructionExample ${RE_SOURCE})
target_include_directories(ReconstructionExample PRIVATE ${CMAKE_SOURCE_DIR})
target_link_libraries(ReconstructionExample PRIVATE ${PNG_LIBRARIES})

add_executable(PointsToDisks ${PTD_SOURCE})
target_include_directories(PointsToDisks PRIVATE ${CMAKE_SOURCE_DIR})

set_target_properties(PoissonRecon PoissonReconClient PoissonReconServer SSDRecon PointInterpolant SurfaceTrimmer EDTInHeat ImageStitching AdaptiveTreeVisualization ChunkPLY ReconstructionExample PointsToDisks
    PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${BIN_DIR})