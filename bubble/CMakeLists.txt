cmake_minimum_required(VERSION 2.8)

if(NOT DEFINED CMAKE_TOOLCHAIN_FILE)
  if(DEFINED ENV{VITASDK})
    set(CMAKE_TOOLCHAIN_FILE "$ENV{VITASDK}/share/vita.toolchain.cmake" CACHE PATH "toolchain file")
  else()
    message(FATAL_ERROR "Please define VITASDK to point to your SDK path!")
  endif()
endif()

project(adrenaline)
include("${VITASDK}/share/vita.cmake" REQUIRED)
set(VITA_APP_NAME "Adrenaline")
set(VITA_TITLEID  "PSPEMUCFW")

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wl,-q -Wall -O3")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fno-rtti -fno-exceptions")
set(VITA_MAKE_FSELF_FLAGS "${VITA_MAKE_FSELF_FLAGS} -a 0x2800000000000001")

add_executable(adrenaline
  main.c
  utils.c
  scr_printf.c
  font.c
)

target_link_libraries(adrenaline
  taihen_stub
  SceAppMgr_stub
  SceCtrl_stub
  SceDisplay_stub
  SceHttp_stub
  SceNet_stub
  SceNetCtl_stub
  SceSysmodule_stub
  ScePgf_stub_weak
)

vita_create_self(eboot.bin adrenaline UNSAFE)
vita_create_vpk(Adrenaline.vpk ${VITA_TITLEID} eboot.bin
  VERSION ${VITA_VERSION}
  NAME ${VITA_APP_NAME}
  FILE pkg/eboot.pbp eboot.pbp
        pkg/flash0/codepage/cptbl.dat flash0/codepage/cptbl.dat
        pkg/flash0/data/cert/CA_LIST.cer flash0/data/cert/CA_LIST.cer
        pkg/flash0/dic/apotp.dic flash0/dic/apotp.dic
        pkg/flash0/dic/atokp.dic flash0/dic/atokp.dic
        pkg/flash0/dic/aux0.dic flash0/dic/aux0.dic
        pkg/flash0/dic/aux1.dic flash0/dic/aux1.dic
        pkg/flash0/dic/aux2.dic flash0/dic/aux2.dic
        pkg/flash0/dic/aux3.dic flash0/dic/aux3.dic
        pkg/flash0/font/arib.pgf flash0/font/arib.pgf
        pkg/flash0/font/gb3s1518.bwfon flash0/font/gb3s1518.bwfon
        pkg/flash0/font/imagefont.bin flash0/font/imagefont.bin
        pkg/flash0/font/jpn0.pgf flash0/font/jpn0.pgf
        pkg/flash0/font/kr0.pgf flash0/font/kr0.pgf
        pkg/flash0/font/ltn0.pgf flash0/font/ltn0.pgf
        pkg/flash0/font/ltn1.pgf flash0/font/ltn1.pgf
        pkg/flash0/font/ltn10.pgf flash0/font/ltn10.pgf
        pkg/flash0/font/ltn11.pgf flash0/font/ltn11.pgf
        pkg/flash0/font/ltn12.pgf flash0/font/ltn12.pgf
        pkg/flash0/font/ltn13.pgf flash0/font/ltn13.pgf
        pkg/flash0/font/ltn14.pgf flash0/font/ltn14.pgf
        pkg/flash0/font/ltn15.pgf flash0/font/ltn15.pgf
        pkg/flash0/font/ltn2.pgf flash0/font/ltn2.pgf
        pkg/flash0/font/ltn3.pgf flash0/font/ltn3.pgf
        pkg/flash0/font/ltn4.pgf flash0/font/ltn4.pgf
        pkg/flash0/font/ltn5.pgf flash0/font/ltn5.pgf
        pkg/flash0/font/ltn6.pgf flash0/font/ltn6.pgf
        pkg/flash0/font/ltn7.pgf flash0/font/ltn7.pgf
        pkg/flash0/font/ltn8.pgf flash0/font/ltn8.pgf
        pkg/flash0/font/ltn9.pgf flash0/font/ltn9.pgf
        pkg/flash0/kd/amctrl.prx flash0/kd/amctrl.prx
        pkg/flash0/kd/audiocodec_260.prx flash0/kd/audiocodec_260.prx
        pkg/flash0/kd/cert_loader.prx flash0/kd/cert_loader.prx
        pkg/flash0/kd/chkreg.prx flash0/kd/chkreg.prx
        pkg/flash0/kd/chnnlsv.prx flash0/kd/chnnlsv.prx
        pkg/flash0/kd/codepage.prx flash0/kd/codepage.prx
        pkg/flash0/kd/g729.prx flash0/kd/g729.prx
        pkg/flash0/kd/http_storage.prx flash0/kd/http_storage.prx
        pkg/flash0/kd/ifhandle.prx flash0/kd/ifhandle.prx
        pkg/flash0/kd/impose_01g.prx flash0/kd/impose_01g.prx
        pkg/flash0/kd/iofilemgr_dnas.prx flash0/kd/iofilemgr_dnas.prx
        pkg/flash0/kd/isofs.prx flash0/kd/isofs.prx
        pkg/flash0/kd/libaac.prx flash0/kd/libaac.prx
        pkg/flash0/kd/libasfparser.prx flash0/kd/libasfparser.prx
        pkg/flash0/kd/libatrac3plus.prx flash0/kd/libatrac3plus.prx
        pkg/flash0/kd/libaudiocodec2.prx flash0/kd/libaudiocodec2.prx
        pkg/flash0/kd/libdnas.prx flash0/kd/libdnas.prx
        pkg/flash0/kd/libdnas_core.prx flash0/kd/libdnas_core.prx
        pkg/flash0/kd/libgameupdate.prx flash0/kd/libgameupdate.prx
        pkg/flash0/kd/libhttp.prx flash0/kd/libhttp.prx
        pkg/flash0/kd/libmp3.prx flash0/kd/libmp3.prx
        pkg/flash0/kd/libmp4.prx flash0/kd/libmp4.prx
        pkg/flash0/kd/libparse_http.prx flash0/kd/libparse_http.prx
        pkg/flash0/kd/libparse_uri.prx flash0/kd/libparse_uri.prx
        pkg/flash0/kd/libssl.prx flash0/kd/libssl.prx
        pkg/flash0/kd/libupdown.prx flash0/kd/libupdown.prx
        pkg/flash0/kd/mcctrl.prx flash0/kd/mcctrl.prx
        pkg/flash0/kd/mediaman.prx flash0/kd/mediaman.prx
        pkg/flash0/kd/mediasync.prx flash0/kd/mediasync.prx
        pkg/flash0/kd/memab.prx flash0/kd/memab.prx
        pkg/flash0/kd/mgvideo.prx flash0/kd/mgvideo.prx
        pkg/flash0/kd/mlnbridge.prx flash0/kd/mlnbridge.prx
        pkg/flash0/kd/mlnbridge_msapp.prx flash0/kd/mlnbridge_msapp.prx
        pkg/flash0/kd/mp4msv.prx flash0/kd/mp4msv.prx
        pkg/flash0/kd/mpeg.prx flash0/kd/mpeg.prx
        pkg/flash0/kd/np.prx flash0/kd/np.prx
        pkg/flash0/kd/np9660.prx flash0/kd/np9660.prx
        pkg/flash0/kd/np_auth.prx flash0/kd/np_auth.prx
        pkg/flash0/kd/np_campaign.prx flash0/kd/np_campaign.prx
        pkg/flash0/kd/np_commerce2.prx flash0/kd/np_commerce2.prx
        pkg/flash0/kd/np_commerce2_regcam.prx flash0/kd/np_commerce2_regcam.prx
        pkg/flash0/kd/np_commerce2_store.prx flash0/kd/np_commerce2_store.prx
        pkg/flash0/kd/np_core.prx flash0/kd/np_core.prx
        pkg/flash0/kd/np_inst.prx flash0/kd/np_inst.prx
        pkg/flash0/kd/np_matching2.prx flash0/kd/np_matching2.prx
        pkg/flash0/kd/np_service.prx flash0/kd/np_service.prx
        pkg/flash0/kd/npdrm.prx flash0/kd/npdrm.prx
        pkg/flash0/kd/openpsid.prx flash0/kd/openpsid.prx
        pkg/flash0/kd/psheet.prx flash0/kd/psheet.prx
        pkg/flash0/kd/registry.prx flash0/kd/registry.prx
        pkg/flash0/kd/resource/impose.rsc flash0/kd/resource/impose.rsc
        pkg/flash0/kd/sc_sascore.prx flash0/kd/sc_sascore.prx
        pkg/flash0/kd/semawm.prx flash0/kd/semawm.prx
        pkg/flash0/kd/sircs.prx flash0/kd/sircs.prx
        pkg/flash0/kd/usersystemlib.prx flash0/kd/usersystemlib.prx
        pkg/flash0/kd/utility.prx flash0/kd/utility.prx
        pkg/flash0/kd/vaudio.prx flash0/kd/vaudio.prx
        pkg/flash0/kd/videocodec_260.prx flash0/kd/videocodec_260.prx
        pkg/flash0/kd/vshbridge.prx flash0/kd/vshbridge.prx
        pkg/flash0/kd/vshbridge_msapp.prx flash0/kd/vshbridge_msapp.prx
        pkg/flash0/vsh/etc/version.txt flash0/vsh/etc/version.txt
        pkg/flash0/vsh/module/adhoc_transfer.prx flash0/vsh/module/adhoc_transfer.prx
        pkg/flash0/vsh/module/auth_plugin.prx flash0/vsh/module/auth_plugin.prx
        pkg/flash0/vsh/module/auto_connect.prx flash0/vsh/module/auto_connect.prx
        pkg/flash0/vsh/module/camera_plugin.prx flash0/vsh/module/camera_plugin.prx
        pkg/flash0/vsh/module/common_gui.prx flash0/vsh/module/common_gui.prx
        pkg/flash0/vsh/module/common_util.prx flash0/vsh/module/common_util.prx
        pkg/flash0/vsh/module/content_browser.prx flash0/vsh/module/content_browser.prx
        pkg/flash0/vsh/module/dd_helper.prx flash0/vsh/module/dd_helper.prx
        pkg/flash0/vsh/module/dd_helper_utility.prx flash0/vsh/module/dd_helper_utility.prx
        pkg/flash0/vsh/module/dialogmain.prx flash0/vsh/module/dialogmain.prx
        pkg/flash0/vsh/module/dnas_plugin.prx flash0/vsh/module/dnas_plugin.prx
        pkg/flash0/vsh/module/file_parser_base.prx flash0/vsh/module/file_parser_base.prx
        pkg/flash0/vsh/module/game_install_plugin.prx flash0/vsh/module/game_install_plugin.prx
        pkg/flash0/vsh/module/game_plugin.prx flash0/vsh/module/game_plugin.prx
        pkg/flash0/vsh/module/htmlviewer_plugin.prx flash0/vsh/module/htmlviewer_plugin.prx
        pkg/flash0/vsh/module/htmlviewer_ui.prx flash0/vsh/module/htmlviewer_ui.prx
        pkg/flash0/vsh/module/htmlviewer_utility.prx flash0/vsh/module/htmlviewer_utility.prx
        pkg/flash0/vsh/module/hvauth_r.prx flash0/vsh/module/hvauth_r.prx
        pkg/flash0/vsh/module/impose_plugin.prx flash0/vsh/module/impose_plugin.prx
        pkg/flash0/vsh/module/launcher_plugin.prx flash0/vsh/module/launcher_plugin.prx
        pkg/flash0/vsh/module/lftv_main_plugin.prx flash0/vsh/module/lftv_main_plugin.prx
        pkg/flash0/vsh/module/lftv_middleware.prx flash0/vsh/module/lftv_middleware.prx
        pkg/flash0/vsh/module/lftv_plugin.prx flash0/vsh/module/lftv_plugin.prx
        pkg/flash0/vsh/module/libfont_arib.prx flash0/vsh/module/libfont_arib.prx
        pkg/flash0/vsh/module/libfont_hv.prx flash0/vsh/module/libfont_hv.prx
        pkg/flash0/vsh/module/libpspvmc.prx flash0/vsh/module/libpspvmc.prx
        pkg/flash0/vsh/module/libslim.prx flash0/vsh/module/libslim.prx
        pkg/flash0/vsh/module/libwww.prx flash0/vsh/module/libwww.prx
        pkg/flash0/vsh/module/marlindownloader.prx flash0/vsh/module/marlindownloader.prx
        pkg/flash0/vsh/module/mcore.prx flash0/vsh/module/mcore.prx
        pkg/flash0/vsh/module/mlnapp_proxy.prx flash0/vsh/module/mlnapp_proxy.prx
        pkg/flash0/vsh/module/mlnbb.prx flash0/vsh/module/mlnbb.prx
        pkg/flash0/vsh/module/mlncmn.prx flash0/vsh/module/mlncmn.prx
        pkg/flash0/vsh/module/mlnusb.prx flash0/vsh/module/mlnusb.prx
        pkg/flash0/vsh/module/mm_flash.prx flash0/vsh/module/mm_flash.prx
        pkg/flash0/vsh/module/msgdialog_plugin.prx flash0/vsh/module/msgdialog_plugin.prx
        pkg/flash0/vsh/module/msvideo_main_plugin.prx flash0/vsh/module/msvideo_main_plugin.prx
        pkg/flash0/vsh/module/msvideo_plugin.prx flash0/vsh/module/msvideo_plugin.prx
        pkg/flash0/vsh/module/music_browser.prx flash0/vsh/module/music_browser.prx
        pkg/flash0/vsh/module/music_main_plugin.prx flash0/vsh/module/music_main_plugin.prx
        pkg/flash0/vsh/module/music_parser.prx flash0/vsh/module/music_parser.prx
        pkg/flash0/vsh/module/music_player.prx flash0/vsh/module/music_player.prx
        pkg/flash0/vsh/module/netconf_plugin_auto_bfl.prx flash0/vsh/module/netconf_plugin_auto_bfl.prx
        pkg/flash0/vsh/module/netconf_plugin_auto_nec.prx flash0/vsh/module/netconf_plugin_auto_nec.prx
        pkg/flash0/vsh/module/netfront.prx flash0/vsh/module/netfront.prx
        pkg/flash0/vsh/module/netplay_client_plugin.prx flash0/vsh/module/netplay_client_plugin.prx
        pkg/flash0/vsh/module/netplay_server2_utility.prx flash0/vsh/module/netplay_server2_utility.prx
        pkg/flash0/vsh/module/netplay_server_plus_utility.prx flash0/vsh/module/netplay_server_plus_utility.prx
        pkg/flash0/vsh/module/netplay_server_utility.prx flash0/vsh/module/netplay_server_utility.prx
        pkg/flash0/vsh/module/npadmin_plugin.prx flash0/vsh/module/npadmin_plugin.prx
        pkg/flash0/vsh/module/npinstaller_plugin.prx flash0/vsh/module/npinstaller_plugin.prx
        pkg/flash0/vsh/module/npsignin_plugin.prx flash0/vsh/module/npsignin_plugin.prx
        pkg/flash0/vsh/module/npsignup_plugin.prx flash0/vsh/module/npsignup_plugin.prx
        pkg/flash0/vsh/module/oneseg_core.prx flash0/vsh/module/oneseg_core.prx
        pkg/flash0/vsh/module/oneseg_hal_toolbox.prx flash0/vsh/module/oneseg_hal_toolbox.prx
        pkg/flash0/vsh/module/oneseg_launcher_plugin.prx flash0/vsh/module/oneseg_launcher_plugin.prx
        pkg/flash0/vsh/module/oneseg_plugin.prx flash0/vsh/module/oneseg_plugin.prx
        pkg/flash0/vsh/module/oneseg_sal.prx flash0/vsh/module/oneseg_sal.prx
        pkg/flash0/vsh/module/oneseg_sdk.prx flash0/vsh/module/oneseg_sdk.prx
        pkg/flash0/vsh/module/oneseg_sdkcore.prx flash0/vsh/module/oneseg_sdkcore.prx
        pkg/flash0/vsh/module/opening_plugin.prx flash0/vsh/module/opening_plugin.prx
        pkg/flash0/vsh/module/osk_plugin.prx flash0/vsh/module/osk_plugin.prx
        pkg/flash0/vsh/module/paf.prx flash0/vsh/module/paf.prx
        pkg/flash0/vsh/module/pafmini.prx flash0/vsh/module/pafmini.prx
        pkg/flash0/vsh/module/photo_browser.prx flash0/vsh/module/photo_browser.prx
        pkg/flash0/vsh/module/photo_main_plugin.prx flash0/vsh/module/photo_main_plugin.prx
        pkg/flash0/vsh/module/photo_player.prx flash0/vsh/module/photo_player.prx
        pkg/flash0/vsh/module/premo_plugin.prx flash0/vsh/module/premo_plugin.prx
        pkg/flash0/vsh/module/ps3scan_plugin.prx flash0/vsh/module/ps3scan_plugin.prx
        pkg/flash0/vsh/module/psn_plugin.prx flash0/vsh/module/psn_plugin.prx
        pkg/flash0/vsh/module/psn_utility.prx flash0/vsh/module/psn_utility.prx
        pkg/flash0/vsh/module/radioshack_plugin.prx flash0/vsh/module/radioshack_plugin.prx
        pkg/flash0/vsh/module/recommend_browser.prx flash0/vsh/module/recommend_browser.prx
        pkg/flash0/vsh/module/recommend_launcher_plugin.prx flash0/vsh/module/recommend_launcher_plugin.prx
        pkg/flash0/vsh/module/recommend_main.prx flash0/vsh/module/recommend_main.prx
        pkg/flash0/vsh/module/rss_browser.prx flash0/vsh/module/rss_browser.prx
        pkg/flash0/vsh/module/rss_common.prx flash0/vsh/module/rss_common.prx
        pkg/flash0/vsh/module/rss_downloader.prx flash0/vsh/module/rss_downloader.prx
        pkg/flash0/vsh/module/rss_main_plugin.prx flash0/vsh/module/rss_main_plugin.prx
        pkg/flash0/vsh/module/rss_reader.prx flash0/vsh/module/rss_reader.prx
        pkg/flash0/vsh/module/rss_subscriber.prx flash0/vsh/module/rss_subscriber.prx
        pkg/flash0/vsh/module/savedata_auto_dialog.prx flash0/vsh/module/savedata_auto_dialog.prx
        pkg/flash0/vsh/module/savedata_plugin.prx flash0/vsh/module/savedata_plugin.prx
        pkg/flash0/vsh/module/savedata_utility.prx flash0/vsh/module/savedata_utility.prx
        pkg/flash0/vsh/module/screenshot_plugin.prx flash0/vsh/module/screenshot_plugin.prx
        pkg/flash0/vsh/module/skype_main_plugin.prx flash0/vsh/module/skype_main_plugin.prx
        pkg/flash0/vsh/module/skype_plugin.prx flash0/vsh/module/skype_plugin.prx
        pkg/flash0/vsh/module/skype_skyhost.prx flash0/vsh/module/skype_skyhost.prx
        pkg/flash0/vsh/module/skype_ve.prx flash0/vsh/module/skype_ve.prx
        pkg/flash0/vsh/module/store_browser_plugin.prx flash0/vsh/module/store_browser_plugin.prx
        pkg/flash0/vsh/module/store_checkout_plugin.prx flash0/vsh/module/store_checkout_plugin.prx
        pkg/flash0/vsh/module/store_checkout_utility.prx flash0/vsh/module/store_checkout_utility.prx
        pkg/flash0/vsh/module/subs_plugin.prx flash0/vsh/module/subs_plugin.prx
        pkg/flash0/vsh/module/sysconf_plugin.prx flash0/vsh/module/sysconf_plugin.prx
        pkg/flash0/vsh/module/update_plugin.prx flash0/vsh/module/update_plugin.prx
        pkg/flash0/vsh/module/video_main_plugin.prx flash0/vsh/module/video_main_plugin.prx
        pkg/flash0/vsh/module/video_plugin.prx flash0/vsh/module/video_plugin.prx
        pkg/flash0/vsh/module/visualizer_plugin.prx flash0/vsh/module/visualizer_plugin.prx
        pkg/flash0/vsh/module/vshmain.prx flash0/vsh/module/vshmain.prx
        pkg/flash0/vsh/resource/01-12.bmp flash0/vsh/resource/01-12.bmp
        pkg/flash0/vsh/resource/01-12_03g.bmp flash0/vsh/resource/01-12_03g.bmp
        pkg/flash0/vsh/resource/13-27.bmp flash0/vsh/resource/13-27.bmp
        pkg/flash0/vsh/resource/adhoc_transfer.rco flash0/vsh/resource/adhoc_transfer.rco
        pkg/flash0/vsh/resource/auth_plugin.rco flash0/vsh/resource/auth_plugin.rco
        pkg/flash0/vsh/resource/camera_plugin.rco flash0/vsh/resource/camera_plugin.rco
        pkg/flash0/vsh/resource/common_page.rco flash0/vsh/resource/common_page.rco
        pkg/flash0/vsh/resource/content_browser_plugin.rco flash0/vsh/resource/content_browser_plugin.rco
        pkg/flash0/vsh/resource/custom_theme.dat flash0/vsh/resource/custom_theme.dat
        pkg/flash0/vsh/resource/dd_helper.rco flash0/vsh/resource/dd_helper.rco
        pkg/flash0/vsh/resource/dnas_plugin.rco flash0/vsh/resource/dnas_plugin.rco
        pkg/flash0/vsh/resource/game_install_plugin.rco flash0/vsh/resource/game_install_plugin.rco
        pkg/flash0/vsh/resource/game_plugin.rco flash0/vsh/resource/game_plugin.rco
        pkg/flash0/vsh/resource/gameboot.pmf flash0/vsh/resource/gameboot.pmf
        pkg/flash0/vsh/resource/htmlviewer.res flash0/vsh/resource/htmlviewer.res
        pkg/flash0/vsh/resource/htmlviewer_plugin.rco flash0/vsh/resource/htmlviewer_plugin.rco
        pkg/flash0/vsh/resource/impose_plugin.rco flash0/vsh/resource/impose_plugin.rco
        pkg/flash0/vsh/resource/lftv_main_plugin.rco flash0/vsh/resource/lftv_main_plugin.rco
        pkg/flash0/vsh/resource/lftv_rmc_univer3in1.rco flash0/vsh/resource/lftv_rmc_univer3in1.rco
        pkg/flash0/vsh/resource/lftv_rmc_univer3in1_jp.rco flash0/vsh/resource/lftv_rmc_univer3in1_jp.rco
        pkg/flash0/vsh/resource/lftv_rmc_univerpanel.rco flash0/vsh/resource/lftv_rmc_univerpanel.rco
        pkg/flash0/vsh/resource/lftv_rmc_univerpanel_jp.rco flash0/vsh/resource/lftv_rmc_univerpanel_jp.rco
        pkg/flash0/vsh/resource/lftv_rmc_univertuner.rco flash0/vsh/resource/lftv_rmc_univertuner.rco
        pkg/flash0/vsh/resource/lftv_rmc_univertuner_jp.rco flash0/vsh/resource/lftv_rmc_univertuner_jp.rco
        pkg/flash0/vsh/resource/lftv_tuner_jp_jp.rco flash0/vsh/resource/lftv_tuner_jp_jp.rco
        pkg/flash0/vsh/resource/lftv_tuner_us_en.rco flash0/vsh/resource/lftv_tuner_us_en.rco
        pkg/flash0/vsh/resource/msgdialog_plugin.rco flash0/vsh/resource/msgdialog_plugin.rco
        pkg/flash0/vsh/resource/msvideo_main_plugin.rco flash0/vsh/resource/msvideo_main_plugin.rco
        pkg/flash0/vsh/resource/music_browser_plugin.rco flash0/vsh/resource/music_browser_plugin.rco
        pkg/flash0/vsh/resource/music_player_plugin.rco flash0/vsh/resource/music_player_plugin.rco
        pkg/flash0/vsh/resource/netconf_dialog.rco flash0/vsh/resource/netconf_dialog.rco
        pkg/flash0/vsh/resource/netplay_plugin.rco flash0/vsh/resource/netplay_plugin.rco
        pkg/flash0/vsh/resource/npadmin_plugin.rco flash0/vsh/resource/npadmin_plugin.rco
        pkg/flash0/vsh/resource/npinstaller_plugin.rco flash0/vsh/resource/npinstaller_plugin.rco
        pkg/flash0/vsh/resource/npsignin_plugin.rco flash0/vsh/resource/npsignin_plugin.rco
        pkg/flash0/vsh/resource/npsignup_plugin.rco flash0/vsh/resource/npsignup_plugin.rco
        pkg/flash0/vsh/resource/oneseg_plugin.rco flash0/vsh/resource/oneseg_plugin.rco
        pkg/flash0/vsh/resource/opening_plugin.rco flash0/vsh/resource/opening_plugin.rco
        pkg/flash0/vsh/resource/osk_plugin.rco flash0/vsh/resource/osk_plugin.rco
        pkg/flash0/vsh/resource/photo_browser_plugin.rco flash0/vsh/resource/photo_browser_plugin.rco
        pkg/flash0/vsh/resource/photo_player_plugin.rco flash0/vsh/resource/photo_player_plugin.rco
        pkg/flash0/vsh/resource/premo_plugin.rco flash0/vsh/resource/premo_plugin.rco
        pkg/flash0/vsh/resource/ps3scan_plugin.rco flash0/vsh/resource/ps3scan_plugin.rco
        pkg/flash0/vsh/resource/psn_plugin.rco flash0/vsh/resource/psn_plugin.rco
        pkg/flash0/vsh/resource/radioshack_plugin.rco flash0/vsh/resource/radioshack_plugin.rco
        pkg/flash0/vsh/resource/recommend_browser.rco flash0/vsh/resource/recommend_browser.rco
        pkg/flash0/vsh/resource/rss_browser_plugin.rco flash0/vsh/resource/rss_browser_plugin.rco
        pkg/flash0/vsh/resource/rss_downloader_plugin.rco flash0/vsh/resource/rss_downloader_plugin.rco
        pkg/flash0/vsh/resource/rss_subscriber.rco flash0/vsh/resource/rss_subscriber.rco
        pkg/flash0/vsh/resource/savedata_plugin.rco flash0/vsh/resource/savedata_plugin.rco
        pkg/flash0/vsh/resource/savedata_utility.rco flash0/vsh/resource/savedata_utility.rco
        pkg/flash0/vsh/resource/screenshot_plugin.rco flash0/vsh/resource/screenshot_plugin.rco
        pkg/flash0/vsh/resource/skype_main_plugin.rco flash0/vsh/resource/skype_main_plugin.rco
        pkg/flash0/vsh/resource/store_browser_plugin.rco flash0/vsh/resource/store_browser_plugin.rco
        pkg/flash0/vsh/resource/store_checkout_plugin.rco flash0/vsh/resource/store_checkout_plugin.rco
        pkg/flash0/vsh/resource/subs_plugin.rco flash0/vsh/resource/subs_plugin.rco
        pkg/flash0/vsh/resource/sysconf_plugin.rco flash0/vsh/resource/sysconf_plugin.rco
        pkg/flash0/vsh/resource/sysconf_plugin_about.rco flash0/vsh/resource/sysconf_plugin_about.rco
        pkg/flash0/vsh/resource/system_plugin.rco flash0/vsh/resource/system_plugin.rco
        pkg/flash0/vsh/resource/system_plugin_bg.rco flash0/vsh/resource/system_plugin_bg.rco
        pkg/flash0/vsh/resource/system_plugin_fg.rco flash0/vsh/resource/system_plugin_fg.rco
        pkg/flash0/vsh/resource/topmenu_icon.rco flash0/vsh/resource/topmenu_icon.rco
        pkg/flash0/vsh/resource/topmenu_plugin.rco flash0/vsh/resource/topmenu_plugin.rco
        pkg/flash0/vsh/resource/update_plugin.rco flash0/vsh/resource/update_plugin.rco
        pkg/flash0/vsh/resource/video_main_plugin.rco flash0/vsh/resource/video_main_plugin.rco
        pkg/flash0/vsh/resource/video_plugin_videotoolbar.rco flash0/vsh/resource/video_plugin_videotoolbar.rco
        pkg/flash0/vsh/resource/visualizer_plugin.rco flash0/vsh/resource/visualizer_plugin.rco
        pkg/flash1/config.adrenaline flash1/config.adrenaline
        pkg/flash1/registry/system.dreg flash1/registry/system.dreg
        pkg/flash1/registry/system.ireg flash1/registry/system.ireg
        pkg/sce_module/adrenaline_kernel.skprx sce_module/adrenaline_kernel.skprx
        pkg/sce_module/adrenaline_user.suprx sce_module/adrenaline_user.suprx
        pkg/sce_module/adrenaline_vsh.suprx sce_module/adrenaline_vsh.suprx
        pkg/sce_module/usbdevice.skprx sce_module/usbdevice.skprx
        pkg/sce_sys/icon0.png sce_sys/icon0.png
        pkg/sce_sys/livearea/contents/bg.png sce_sys/livearea/contents/bg.png
        pkg/sce_sys/livearea/contents/startup.png sce_sys/livearea/contents/startup.png
        pkg/sce_sys/livearea/contents/template.xml sce_sys/livearea/contents/template.xml
)

add_custom_target(copy
  COMMAND cp eboot.bin F:/app/${VITA_TITLEID}/eboot.bin
  DEPENDS eboot.bin
)