cmake_minimum_required( VERSION 3.16 )

project( ccbLib CXX C )

set( CMAKE_CXX_STANDARD 11 )

add_library(irrlicht STATIC)


include_directories(source/Irrlicht/libpng)
include_directories(source/Irrlicht/jpeglib)
include_directories(source/Irrlicht/zlib)

add_subdirectory(source/Irrlicht/libpng)
add_subdirectory(source/Irrlicht/jpeglib)
add_subdirectory(source/Irrlicht/zlib)

target_sources(
        irrlicht PRIVATE
        source/Irrlicht/C3DSMeshFileLoader.cpp
        source/Irrlicht/CAnimatedMeshMD2.cpp
        source/Irrlicht/CAnimatedMeshMD3.cpp
        source/Irrlicht/CAnimatedMeshSceneNode.cpp
        source/Irrlicht/CAttributes.cpp
        source/Irrlicht/CB3DMeshFileLoader.cpp
        source/Irrlicht/CBillboardSceneNode.cpp
        source/Irrlicht/CBoneSceneNode.cpp
        source/Irrlicht/CBSPMeshFileLoader.cpp
        source/Irrlicht/CCameraFPSSceneNode.cpp
        source/Irrlicht/CCameraMayaSceneNode.cpp
        source/Irrlicht/CCameraSceneNode.cpp
        source/Irrlicht/CColladaFileLoader.cpp
        source/Irrlicht/CColladaMeshWriter.cpp
        source/Irrlicht/CColorConverter.cpp
        source/Irrlicht/CCSMLoader.cpp
        source/Irrlicht/CCSMLoader.cpp
        source/Irrlicht/CCubeSceneNode.cpp
        source/Irrlicht/CDefaultGUIElementFactory.cpp
        source/Irrlicht/CDefaultSceneNodeAnimatorFactory.cpp
        source/Irrlicht/CDefaultSceneNodeFactory.cpp
        source/Irrlicht/CDepthBuffer.cpp
        source/Irrlicht/CDMFLoader.cpp
        source/Irrlicht/CDummyTransformationSceneNode.cpp
        source/Irrlicht/CEmptySceneNode.cpp
        source/Irrlicht/CFileList.cpp
        source/Irrlicht/CFileSystem.cpp
        source/Irrlicht/CFPSCounter.cpp
        source/Irrlicht/CGeometryCreator.cpp
        source/Irrlicht/CGUIButton.cpp
        source/Irrlicht/CGUICheckBox.cpp
        source/Irrlicht/CGUIColorSelectDialog.cpp
        source/Irrlicht/CGUIComboBox.cpp
        source/Irrlicht/CGUIContextMenu.cpp
        source/Irrlicht/CGUIEditBox.cpp
        source/Irrlicht/CGUIEnvironment.cpp
        source/Irrlicht/CGUIFileOpenDialog.cpp
        source/Irrlicht/CGUIFont.cpp
        source/Irrlicht/CGUIImage.cpp
        source/Irrlicht/CGUIInOutFader.cpp
        source/Irrlicht/CGUIListBox.cpp
        source/Irrlicht/CGUIMenu.cpp
        source/Irrlicht/CGUIMeshViewer.cpp
        source/Irrlicht/CGUIMessageBox.cpp
        source/Irrlicht/CGUIModalScreen.cpp
        source/Irrlicht/CGUIScrollBar.cpp
        source/Irrlicht/CGUISkin.cpp
        source/Irrlicht/CGUISpinBox.cpp
        source/Irrlicht/CGUISpriteBank.cpp
        source/Irrlicht/CGUIStaticText.cpp
        source/Irrlicht/CGUITabControl.cpp
        source/Irrlicht/CGUITable.cpp
        source/Irrlicht/CGUIToolBar.cpp
        source/Irrlicht/CGUIWindow.cpp
        source/Irrlicht/CImage.cpp
        source/Irrlicht/CImageLoaderBMP.cpp
        source/Irrlicht/CImageLoaderJPG.cpp
        source/Irrlicht/CImageLoaderPCX.cpp
        source/Irrlicht/CImageLoaderPNG.cpp
        source/Irrlicht/CImageLoaderPPM.cpp
        source/Irrlicht/CImageLoaderPSD.cpp
        source/Irrlicht/CImageLoaderTGA.cpp
        source/Irrlicht/CImageLoaderWAL.cpp
        source/Irrlicht/CIrrDeviceStub.cpp
        source/Irrlicht/CIrrMeshFileLoader.cpp
        source/Irrlicht/CIrrMeshWriter.cpp
        source/Irrlicht/CLightSceneNode.cpp
        source/Irrlicht/CLimitReadFile.cpp
        source/Irrlicht/CLMTSMeshFileLoader.cpp
        source/Irrlicht/CLogger.cpp
        source/Irrlicht/CLWOMeshFileLoader.cpp
        source/Irrlicht/CMD2MeshFileLoader.cpp
        source/Irrlicht/CMD3MeshFileLoader.cpp
        source/Irrlicht/CMemoryReadFile.cpp
        source/Irrlicht/CMeshCache.cpp
        source/Irrlicht/CMeshManipulator.cpp
        source/Irrlicht/CMeshSceneNode.cpp
        source/Irrlicht/CMetaTriangleSelector.cpp
        source/Irrlicht/CMS3DMeshFileLoader.cpp
        source/Irrlicht/CMY3DMeshFileLoader.cpp
        source/Irrlicht/CNullDriver.cpp
        source/Irrlicht/COBJMeshFileLoader.cpp
        source/Irrlicht/COBJMeshWriter.cpp
        source/Irrlicht/COCTLoader.cpp
        source/Irrlicht/COctTreeSceneNode.cpp
        source/Irrlicht/COctTreeTriangleSelector.cpp
        source/Irrlicht/COgreMeshFileLoader.cpp
        source/Irrlicht/COSOperator.cpp
        source/Irrlicht/CPakReader.cpp
        source/Irrlicht/CParticleAnimatedMeshSceneNodeEmitter.cpp
        source/Irrlicht/CParticleAttractionAffector.cpp
        source/Irrlicht/CParticleBoxEmitter.cpp
        source/Irrlicht/CParticleCylinderEmitter.cpp
        source/Irrlicht/CParticleFadeOutAffector.cpp
        source/Irrlicht/CParticleGravityAffector.cpp
        source/Irrlicht/CParticleMeshEmitter.cpp
        source/Irrlicht/CParticlePointEmitter.cpp
        source/Irrlicht/CParticleRingEmitter.cpp
        source/Irrlicht/CParticleRotationAffector.cpp
        source/Irrlicht/CParticleScaleAffector.cpp
        source/Irrlicht/CParticleSphereEmitter.cpp
        source/Irrlicht/CParticleSystemSceneNode.cpp
        source/Irrlicht/CQ3LevelMesh.cpp
        source/Irrlicht/CQuake3ShaderSceneNode.cpp
        source/Irrlicht/CReadFile.cpp
        source/Irrlicht/CSceneCollisionManager.cpp
        source/Irrlicht/CSceneManager.cpp
        source/Irrlicht/CSceneNodeAnimatorCameraFPS.cpp
        source/Irrlicht/CSceneNodeAnimatorCameraMaya.cpp
        source/Irrlicht/CSceneNodeAnimatorCollisionResponse.cpp
        source/Irrlicht/CSceneNodeAnimatorDelete.cpp
        source/Irrlicht/CSceneNodeAnimatorFlyCircle.cpp
        source/Irrlicht/CSceneNodeAnimatorFlyStraight.cpp
        source/Irrlicht/CSceneNodeAnimatorFollowSpline.cpp
        source/Irrlicht/CSceneNodeAnimatorRotation.cpp
        source/Irrlicht/CSceneNodeAnimatorTexture.cpp
        source/Irrlicht/CShadowVolumeSceneNode.cpp
        source/Irrlicht/CSkinnedMesh.cpp
        source/Irrlicht/CSkyBoxSceneNode.cpp
        source/Irrlicht/CSkyDomeSceneNode.cpp
        source/Irrlicht/CSphereSceneNode.cpp
        source/Irrlicht/CSTLMeshFileLoader.cpp
        source/Irrlicht/CSTLMeshWriter.cpp
        source/Irrlicht/CTerrainSceneNode.cpp
        source/Irrlicht/CTerrainTriangleSelector.cpp
        source/Irrlicht/CTextSceneNode.cpp
        source/Irrlicht/CTriangleSelector.cpp
        source/Irrlicht/CTriangleBBSelector.cpp
        source/Irrlicht/CVideoModeList.cpp
        source/Irrlicht/CVolumeLightSceneNode.cpp
        source/Irrlicht/CWaterSurfaceSceneNode.cpp
        source/Irrlicht/CWriteFile.cpp
        source/Irrlicht/CXMeshFileLoader.cpp
        source/Irrlicht/CXMLReader.cpp
        source/Irrlicht/CXMLWriter.cpp
        source/Irrlicht/CZBuffer.cpp
        source/Irrlicht/CZipReader.cpp
        source/Irrlicht/Irrlicht.cpp
        source/Irrlicht/irrXML.cpp
        source/Irrlicht/os.cpp
        source/Irrlicht/CImageWriterBMP.cpp
        source/Irrlicht/CImageWriterJPG.cpp
        source/Irrlicht/CImageWriterPCX.cpp
        source/Irrlicht/CImageWriterPNG.cpp
        source/Irrlicht/CImageWriterPPM.cpp
        source/Irrlicht/CImageWriterPSD.cpp
        source/Irrlicht/CImageWriterTGA.cpp
)



function(LoadOpenGL)
        find_package( OpenGL REQUIRED )
        target_include_directories(irrlicht PRIVATE ${OPENGL_INCLUDE_DIRS})
        target_link_libraries(OpenGL::GL)
        target_sources(
                irrlicht PRIVATE
                source/Irrlicht/COpenGLDriver.cpp
                source/Irrlicht/COpenGLExtensionHandler.cpp
                source/Irrlicht/COpenGLNormalMapRenderer.cpp
                source/Irrlicht/COpenGLParallaxMapRenderer.cpp
                source/Irrlicht/COpenGLShaderMaterialRenderer.cpp
                source/Irrlicht/COpenGLSLMaterialRenderer.cpp
                source/Irrlicht/COpenGLTerrainMaterialRenderer.cpp
                source/Irrlicht/COpenGLTexture.cpp
        )
endfunction()

function(LoadSoftwareDrivers)
        target_sources(
                irrlicht PRIVATE
                source/Irrlicht/CSoftwareDriver.cpp
                source/Irrlicht/CSoftwareDriver2.cpp
                source/Irrlicht/CSoftwareTexture.cpp
                source/Irrlicht/CSoftwareTexture2.cpp
                source/Irrlicht/CTRFlat.cpp
                source/Irrlicht/CTRFlatWire.cpp
                source/Irrlicht/CTRGouraud.cpp
                source/Irrlicht/CTRGouraud2.cpp
                source/Irrlicht/CTRGouraudAlpha2.cpp
                source/Irrlicht/CTRGouraudAlphaNoZ2.cpp
                source/Irrlicht/CTRGouraudWire.cpp
                source/Irrlicht/CTRTextureBlend.cpp
                source/Irrlicht/CTRTextureDetailMap2.cpp
                source/Irrlicht/CTRTextureFlat.cpp
                source/Irrlicht/CTRTextureFlatWire.cpp
                source/Irrlicht/CTRTextureGouraud.cpp
                source/Irrlicht/CTRTextureGouraud2.cpp
                source/Irrlicht/CTRTextureGouraudAdd.cpp
                source/Irrlicht/CTRTextureGouraudAdd2.cpp
                source/Irrlicht/CTRTextureGouraudAddNoZ2.cpp
                source/Irrlicht/CTRTextureGouraudAlpha.cpp
                source/Irrlicht/CTRTextureGouraudAlphaNoZ.cpp
                source/Irrlicht/CTRTextureGouraudNoZ.cpp
                source/Irrlicht/CTRTextureGouraudNoZ2.cpp
                source/Irrlicht/CTRTextureGouraudVertexAlpha2.cpp
                source/Irrlicht/CTRTextureGouraudWire.cpp
                source/Irrlicht/CTRTextureLightMap2_Add.cpp
                source/Irrlicht/CTRTextureLightMap2_M1.cpp
                source/Irrlicht/CTRTextureLightMap2_M2.cpp
                source/Irrlicht/CTRTextureLightMap2_M4.cpp
                source/Irrlicht/CTRTextureLightMapGouraud2_M4.cpp
                source/Irrlicht/CTRTextureWire2.cpp
                source/Irrlicht/CBurningShader_Raster_Reference.cpp
                source/Irrlicht/IBurningShader.cpp
        )
endfunction()


function(LoadDXSDK)
        if(DEFINED ENV{DXSDK_DIR})
                set(DXSDK_INCLUDE_DIRS "$ENV{DXSDK_DIR}/Include")

                if( CMAKE_SIZEOF_VOID_P EQUAL 8 )
                        set(DXSDK_LIBRARY_DIRS "$ENV{DXSDK_DIR}/Lib/x64")
                elseif (CMAKE_SIZEOF_VOID_P EQUAL 4)
                        set(DXSDK_LIBRARY_DIRS "$ENV{DXSDK_DIR}/Lib/x86")
                endif ()

                target_include_directories(irrlicht PUBLIC ${DXSDK_INCLUDE_DIRS})
                target_link_directories(irrlicht PUBLIC ${DXSDK_LIBRARY_DIRS})

                target_sources(
                        irrlicht PRIVATE
                        source/Irrlicht/CD3D9Driver.cpp
                        source/Irrlicht/CD3D9HLSLMaterialRenderer.cpp
                        source/Irrlicht/CD3D9NormalMapRenderer.cpp
                        source/Irrlicht/CD3D9ParallaxMapRenderer.cpp
                        source/Irrlicht/CD3D9ShaderMaterialRenderer.cpp
                        source/Irrlicht/CD3D9Texture.cpp
                )

        else()
                #message(FATAL_ERROR "System variable DXSDK_DIR is not defined. Please set it to the path of the DirectX SDK.")
                message("(Legacy) DirectX SDK not found. Please set the system variable DXSDK_DIR to the path of the DirectX SDK 2010 Redistributable to enable DirectX 9+ support.")
        endif()
endfunction()

if (WIN32)
        target_sources(
                irrlicht PRIVATE
                source/Irrlicht/CIrrDeviceWin32.cpp
                source/Irrlicht/CWin32VideoStreamControl.cpp
        )

        if(MSVC)
                #target_compile_options(irrlicht PUBLIC /utf-8)

                # Check if an environment variable is defined
                if(DEFINED ENV{DXSDK_DIR})
                        message(STATUS "System variable DXSDK_DIR found, loading DirectX SDK...")
                        LoadDXSDK()
                endif ()

        endif ()

elseif (UNIX AND NOT APPLE)
else ()

endif ()

LoadOpenGL()
LoadSoftwareDrivers()

target_include_directories(irrlicht PUBLIC include source/Irrlicht)

target_link_libraries(irrlicht PUBLIC libjpeg zlib libpnglib)
