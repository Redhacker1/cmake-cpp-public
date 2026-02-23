cmake_minimum_required( VERSION 3.16 )

project( ccbLib CXX C )

set( CMAKE_CXX_STANDARD 11 )

add_subdirectory(bullet/src)
add_subdirectory(irrlicht)
add_subdirectory(irrklang)
add_subdirectory(spidermonkey)
add_subdirectory(curl)
# If you bring over the CMakeLists.txt and all the subdirectories from here:
# https://github.com/assimp/assimp/tree/6f0bc9bcb29fa0c9f23e89e2619ba380d2ff18bb
# It should work, theoretically, it might be broken due to age, but it should be fixable,
# AI can do it if you really need it to quite trivially.
#add_subdirectory(assimp) # Not currently used by engine, so not implemented as its a fairly large dependency.

add_library(flacelib STATIC)


target_sources(flacelib PRIVATE
        CBulletBody.cpp
        CBulletPhysicsSimulation.cpp
        CCCActionChangeSceneNodePosition.cpp
        CCCActionChangeSceneNodeRotation.cpp
        CCCActionChangeSceneNodeScale.cpp
        CCCActionChangeSceneNodeTexture.cpp
        CCCActionCloneSceneNode.cpp
        CCCActionDeleteSceneNode.cpp
        CCCActionDoInTheFuture.cpp
        CCCActionExecuteJavaScript.cpp
        CCCActionExtensionScript.cpp
        CCCActionHandler.cpp
        CCCActionIf.cpp
        CCCActionMakeSceneNodeInvisible.cpp
        CCCActionOpenWebpage.cpp
        CCCActionPlayMovie.cpp
        CCCActionPlaySound.cpp
        CCCActionQuitApplication.cpp
        CCCActionReloadScene.cpp
        CCCActionRestartBehaviors.cpp
        CCCActionSetActiveCamera.cpp
        CCCActionSetCameraTarget.cpp
        CCCActionSetOrChangeAVariable.cpp
        CCCActionSetOverlayText.cpp
        CCCActionSetSceneNodeAnimation.cpp
        CCCActionShoot.cpp
        CCCActionStopSound.cpp
        CCCActionStopSpecificSound.cpp
        CCCActionStoreLoadVariable.cpp
        CCCActionSwitchToScene.cpp
        CCCAttributeStrings.cpp
        CCCExtensionScriptProperty.cpp
        CFlace2DMobileInputNode.cpp
        CFlace2DOverlayNode.cpp
        CFlace3DScene.cpp
        CFlace3DSoundSceneNode.cpp
        CFlaceAnimatedMeshSceneNode.cpp
        CFlaceAnimator3rdPersonCamera.cpp
        CFlaceAnimatorAnimateTextures.cpp
        CFlaceAnimatorCameraFPS.cpp
        CFlaceAnimatorCameraModelViewer.cpp
        CFlaceAnimatorCollisionResponse.cpp
        CFlaceAnimatorExtensionScript.cpp
        CFlaceAnimatorFlyCircle.cpp
        CFlaceAnimatorFlyStraight.cpp
        CFlaceAnimatorFollowPath.cpp
        CFlaceAnimatorGameAI.cpp
        CFlaceAnimatorKeyboardControlled.cpp
        CFlaceAnimatorOnClick.cpp
        CFlaceAnimatorOnCollide.cpp
        CFlaceAnimatorOnFirstFrame.cpp
        CFlaceAnimatorOnKeyPress.cpp
        CFlaceAnimatorOnMouseMove.cpp
        CFlaceAnimatorRigidPhysicsBody.cpp
        CFlaceAnimatorRotation.cpp
        CFlaceAnimatorsAll.cpp
        CFlaceAnimatorTimer.cpp
        CFlaceAttributeSerializationHelper.cpp
        CFlaceBillboardSceneNode.cpp
        CFlaceCameraSceneNode.cpp
        CFlaceDeserializer.cpp
        CFlaceDocument.cpp
        CFlaceDummyTransformationSceneNode.cpp
        CFlaceHotspotNode.cpp
        CFlaceLightSceneNode.cpp
        CFlaceMeshSceneNode.cpp
        CFlaceMetaDataContainer.cpp
        CFlaceMetaDataEntryOpenClosed.cpp
        CFlaceMetaDataEntryRoomMesh.cpp
        CFlacePanoramaScene.cpp
        CFlaceParticleSystemSceneNode.cpp
        CFlacePathSceneNode.cpp
        CFlaceScene.cpp
        CFlaceSerializer.cpp
        CFlaceSkyBoxSceneNode.cpp
        CFlaceTerrainSceneNode.cpp
        CFlaceTreeGenerator.cpp
        CFlaceVariable.cpp
        CFlaceWarningAndErrorReceiver.cpp
        CFlaceWaterSceneNode.cpp
        CImageLoaderDDS.cpp
        CIrrEditServices.cpp
        CODEPhysicsSimulation.cpp
        CMemoryWriteFile.cpp
        CNetworkSupport.cpp
        CSpidermonkeyScriptEngine.cpp
        CSpidermonkeyScriptEngineLib.cpp
        irrHelpers.cpp
        irrUnicodeSupport.cpp
        SFlaceHotspotData.cpp
        SFlacePublishSettings.cpp
        assimp/contrib/ConvertUTF/ConvertUTF.c
)

if(WIN32)
    target_sources(flacelib PRIVATE
            CFlaceWin32FontManager.cpp
            CIrrWin32CriticalSection.cpp
    )
elseif (UNIX)
    target_sources(flacelib PRIVATE
            CIrrLinuxCriticalSection.cpp
    )
endif ()

target_include_directories(flacelib PUBLIC
        include
        irrlicht/include
        ${CMAKE_CURRENT_LIST_DIR}
)

# In Debug builds on Windows, irrKlang is linked as a shared library.
# We handled the selection of static vs shared in flacelib/irrklang/CMakeLists.txt,
# so we can just link to irrKlang here.
target_link_libraries(flacelib PUBLIC
        BulletDynamics
        BulletCollision
        LinearMath
        irrlicht
        irrKlang
        spidermonkey
        libcurl
)

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Release")
endif()