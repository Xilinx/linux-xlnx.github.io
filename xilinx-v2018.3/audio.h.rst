.. -*- coding: utf-8; mode: rst -*-

audio.h
=======

.. parsed-literal::

    \/\* SPDX-License-Identifier\: LGPL-2.1+ WITH Linux-syscall-note \*\/
    \/\*
     \* audio.h
     \*
     \* Copyright (C) 2000 Ralph  Metzler \<ralph@convergence.de\>
     \*                  \& Marcus Metzler \<marcus@convergence.de\>
     \*                    for convergence integrated media GmbH
     \*
     \* This program is free software; you can redistribute it and\/or
     \* modify it under the terms of the GNU General Lesser Public License
     \* as published by the Free Software Foundation; either version 2.1
     \* of the License, or (at your option) any later version.
     \*
     \* This program is distributed in the hope that it will be useful,
     \* but WITHOUT ANY WARRANTY; without even the implied warranty of
     \* MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
     \* GNU General Public License for more details.
     \*
     \* You should have received a copy of the GNU Lesser General Public License
     \* along with this program; if not, write to the Free Software
     \* Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA  02111-1307, USA.
     \*
     \*\/

    \#ifndef \_DVBAUDIO\_H\_
    \#define \_DVBAUDIO\_H\_

    \#include \<linux\/types.h\>

    typedef enum \{
            AUDIO\_SOURCE\_DEMUX, \/\* Select the demux as the main source \*\/
            AUDIO\_SOURCE\_MEMORY \/\* Select internal memory as the main source \*\/
    \} audio\_stream\_source\_t;

    typedef enum \{
            AUDIO\_STOPPED,      \/\* Device is stopped \*\/
            AUDIO\_PLAYING,      \/\* Device is currently playing \*\/
            AUDIO\_PAUSED        \/\* Device is paused \*\/
    \} audio\_play\_state\_t;

    typedef enum \{
            AUDIO\_STEREO,
            AUDIO\_MONO\_LEFT,
            AUDIO\_MONO\_RIGHT,
            AUDIO\_MONO,
            AUDIO\_STEREO\_SWAPPED
    \} audio\_channel\_select\_t;

    typedef struct :c:type:`audio_mixer` \{
            unsigned int volume\_left;
            unsigned int volume\_right;
      \/\/ what else do we need? bass, pass-through, ...
    \} :c:type:`audio_mixer_t <audio_mixer>`;

    typedef struct :c:type:`audio_status` \{
            int                    AV\_sync\_state;  \/\* sync audio and video? \*\/
            int                    mute\_state;     \/\* audio is muted \*\/
            audio\_play\_state\_t     play\_state;     \/\* current playback state \*\/
            audio\_stream\_source\_t  stream\_source;  \/\* current stream source \*\/
            audio\_channel\_select\_t channel\_select; \/\* currently selected channel \*\/
            int                    bypass\_mode;    \/\* pass on audio data to \*\/
            :c:type:`audio_mixer_t <audio_mixer>`          mixer\_state;    \/\* current mixer state \*\/
    \} :c:type:`audio_status_t <audio_status>`;                              \/\* separate decoder hardware \*\/

    typedef
    struct :c:type:`audio_karaoke` \{  \/\* if Vocal1 or Vocal2 are non-zero, they get mixed  \*\/
            int vocal1;    \/\* into left and right t at 70\% each \*\/
            int vocal2;    \/\* if both, Vocal1 and Vocal2 are non-zero, Vocal1 gets\*\/
            int melody;    \/\* mixed into the left channel and \*\/
                           \/\* Vocal2 into the right channel at 100\% each. \*\/
                           \/\* if Melody is non-zero, the melody channel gets mixed\*\/
    \} :c:type:`audio_karaoke_t <audio_karaoke>`;     \/\* into left and right  \*\/

    typedef \_\_u16 audio\_attributes\_t;
    \/\*   bits\: descr. \*\/
    \/\*   15-13 audio coding mode (0=ac3, 2=mpeg1, 3=mpeg2ext, 4=LPCM, 6=DTS, \*\/
    \/\*   12    multichannel extension \*\/
    \/\*   11-10 audio type (0=not spec, 1=language included) \*\/
    \/\*    9- 8 audio application mode (0=not spec, 1=karaoke, 2=surround) \*\/
    \/\*    7- 6 Quantization \/ DRC (mpeg audio\: 1=DRC exists)(lpcm\: 0=16bit,  \*\/
    \/\*    5- 4 Sample frequency fs (0=48kHz, 1=96kHz) \*\/
    \/\*    2- 0 number of audio channels (n+1 channels) \*\/

    \/\* for GET\_CAPABILITIES and SET\_FORMAT, the latter should only set one bit \*\/
    \#define AUDIO\_CAP\_DTS    1
    \#define AUDIO\_CAP\_LPCM   2
    \#define AUDIO\_CAP\_MP1    4
    \#define AUDIO\_CAP\_MP2    8
    \#define AUDIO\_CAP\_MP3   16
    \#define AUDIO\_CAP\_AAC   32
    \#define AUDIO\_CAP\_OGG   64
    \#define AUDIO\_CAP\_SDDS 128
    \#define AUDIO\_CAP\_AC3  256

    \#define \ :ref:`AUDIO_STOP <audio_stop>`                 \_IO('o', 1)
    \#define \ :ref:`AUDIO_PLAY <audio_play>`                 \_IO('o', 2)
    \#define \ :ref:`AUDIO_PAUSE <audio_pause>`                \_IO('o', 3)
    \#define \ :ref:`AUDIO_CONTINUE <audio_continue>`             \_IO('o', 4)
    \#define \ :ref:`AUDIO_SELECT_SOURCE <audio_select_source>`        \_IO('o', 5)
    \#define \ :ref:`AUDIO_SET_MUTE <audio_set_mute>`             \_IO('o', 6)
    \#define \ :ref:`AUDIO_SET_AV_SYNC <audio_set_av_sync>`          \_IO('o', 7)
    \#define \ :ref:`AUDIO_SET_BYPASS_MODE <audio_set_bypass_mode>`      \_IO('o', 8)
    \#define \ :ref:`AUDIO_CHANNEL_SELECT <audio_channel_select>`       \_IO('o', 9)
    \#define \ :ref:`AUDIO_GET_STATUS <audio_get_status>`           \_IOR('o', 10, :c:type:`audio_status_t <audio_status>`)

    \#define \ :ref:`AUDIO_GET_CAPABILITIES <audio_get_capabilities>`     \_IOR('o', 11, unsigned int)
    \#define \ :ref:`AUDIO_CLEAR_BUFFER <audio_clear_buffer>`         \_IO('o',  12)
    \#define \ :ref:`AUDIO_SET_ID <audio_set_id>`               \_IO('o', 13)
    \#define \ :ref:`AUDIO_SET_MIXER <audio_set_mixer>`            \_IOW('o', 14, :c:type:`audio_mixer_t <audio_mixer>`)
    \#define \ :ref:`AUDIO_SET_STREAMTYPE <audio_set_streamtype>`       \_IO('o', 15)
    \#define \ :ref:`AUDIO_SET_EXT_ID <audio_set_ext_id>`           \_IO('o', 16)
    \#define \ :ref:`AUDIO_SET_ATTRIBUTES <audio_set_attributes>`       \_IOW('o', 17, audio\_attributes\_t)
    \#define \ :ref:`AUDIO_SET_KARAOKE <audio_set_karaoke>`          \_IOW('o', 18, :c:type:`audio_karaoke_t <audio_karaoke>`)

    \/\*\*
     \* \ :ref:`AUDIO_GET_PTS <audio_get_pts>`
     \*
     \* Read the 33 bit presentation time stamp as defined
     \* in ITU T-REC-H.222.0 \/ ISO\/IEC 13818-1.
     \*
     \* The PTS should belong to the currently played
     \* frame if possible, but may also be a value close to it
     \* like the PTS of the last decoded frame or the last PTS
     \* extracted by the PES parser.
     \*\/
    \#define \ :ref:`AUDIO_GET_PTS <audio_get_pts>`              \_IOR('o', 19, \_\_u64)
    \#define \ :ref:`AUDIO_BILINGUAL_CHANNEL_SELECT <audio_bilingual_channel_select>` \_IO('o', 20)

    \#endif \/\* \_DVBAUDIO\_H\_ \*\/
