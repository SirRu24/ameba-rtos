#build audio libs
if(CONFIG_AUDIO_FWK)
    ameba_app_library(audio_mixer)
    ameba_app_library(audio_passthrough)
    add_subdirectory(audio_algorithm)
    add_subdirectory(audio_effect)
    add_subdirectory(audio_control)
    add_subdirectory(audio_stream)
    add_subdirectory(base)
endif()

add_subdirectory(third_party)
