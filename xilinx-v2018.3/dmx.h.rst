.. -*- coding: utf-8; mode: rst -*-

dmx.h
=====

.. parsed-literal::

    \/\* SPDX-License-Identifier\: LGPL-2.1+ WITH Linux-syscall-note \*\/
    \/\*
     \* dmx.h
     \*
     \* Copyright (C) 2000 Marcus Metzler \<marcus@convergence.de\>
     \*                  \& Ralph  Metzler \<ralph@convergence.de\>
     \*                    for convergence integrated media GmbH
     \*
     \* This program is free software; you can redistribute it and\/or
     \* modify it under the terms of the GNU Lesser General Public License
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

    \#ifndef \_UAPI\_DVBDMX\_H\_
    \#define \_UAPI\_DVBDMX\_H\_

    \#include \<linux\/types.h\>
    \#ifndef \_\_KERNEL\_\_
    \#include \<time.h\>
    \#endif

    \#define DMX\_FILTER\_SIZE 16

    \/\*\*
     \* enum :c:type:`dmx_output` - Output for the demux.
     \*
     \* @DMX\_OUT\_DECODER\:
     \*      Streaming directly to decoder.
     \* @DMX\_OUT\_TAP\:
     \*      Output going to a memory buffer (to be retrieved via the read command).
     \*      Delivers the stream output to the demux device on which the ioctl
     \*      is called.
     \* @DMX\_OUT\_TS\_TAP\:
     \*      Output multiplexed into a new TS (to be retrieved by reading from the
     \*      logical DVR device). Routes output to the logical DVR device
     \*      \`\`\/dev\/dvb\/adapter?\/dvr?\`\`, which delivers a TS multiplexed from all
     \*      filters for which @DMX\_OUT\_TS\_TAP was specified.
     \* @DMX\_OUT\_TSDEMUX\_TAP\:
     \*      Like @DMX\_OUT\_TS\_TAP but retrieved from the DMX device.
     \*\/
    enum :c:type:`dmx_output` \{
            DMX\_OUT\_DECODER,
            DMX\_OUT\_TAP,
            DMX\_OUT\_TS\_TAP,
            DMX\_OUT\_TSDEMUX\_TAP
    \};

    \/\*\*
     \* :c:type:`dmx_input <dmx_input>` - Input from the demux.
     \*
     \* @:c:type:`DMX_IN_FRONTEND <dmx_input>`\:    Input from a front-end device.
     \* @:c:type:`DMX_IN_DVR <dmx_input>`\:         Input from the logical DVR device.
     \*\/
    :c:type:`dmx_input <dmx_input>` \{
            :c:type:`DMX_IN_FRONTEND <dmx_input>`,
            :c:type:`DMX_IN_DVR <dmx_input>`
    \};

    \/\*\*
     \* :c:type:`dmx_ts_pes <dmx_pes_type>` - type of the PES filter.
     \*
     \* @:c:type:`DMX_PES_AUDIO0 <dmx_pes_type>`\:     first audio PID. Also referred as @DMX\_PES\_AUDIO.
     \* @:c:type:`DMX_PES_VIDEO0 <dmx_pes_type>`\:     first video PID. Also referred as @DMX\_PES\_VIDEO.
     \* @:c:type:`DMX_PES_TELETEXT0 <dmx_pes_type>`\:  first teletext PID. Also referred as @DMX\_PES\_TELETEXT.
     \* @:c:type:`DMX_PES_SUBTITLE0 <dmx_pes_type>`\:  first subtitle PID. Also referred as @DMX\_PES\_SUBTITLE.
     \* @:c:type:`DMX_PES_PCR0 <dmx_pes_type>`\:       first Program Clock Reference PID.
     \*                      Also referred as @DMX\_PES\_PCR.
     \*
     \* @:c:type:`DMX_PES_AUDIO1 <dmx_pes_type>`\:     second audio PID.
     \* @:c:type:`DMX_PES_VIDEO1 <dmx_pes_type>`\:     second video PID.
     \* @:c:type:`DMX_PES_TELETEXT1 <dmx_pes_type>`\:  second teletext PID.
     \* @:c:type:`DMX_PES_SUBTITLE1 <dmx_pes_type>`\:  second subtitle PID.
     \* @:c:type:`DMX_PES_PCR1 <dmx_pes_type>`\:       second Program Clock Reference PID.
     \*
     \* @:c:type:`DMX_PES_AUDIO2 <dmx_pes_type>`\:     third audio PID.
     \* @:c:type:`DMX_PES_VIDEO2 <dmx_pes_type>`\:     third video PID.
     \* @:c:type:`DMX_PES_TELETEXT2 <dmx_pes_type>`\:  third teletext PID.
     \* @:c:type:`DMX_PES_SUBTITLE2 <dmx_pes_type>`\:  third subtitle PID.
     \* @:c:type:`DMX_PES_PCR2 <dmx_pes_type>`\:       third Program Clock Reference PID.
     \*
     \* @:c:type:`DMX_PES_AUDIO3 <dmx_pes_type>`\:     fourth audio PID.
     \* @:c:type:`DMX_PES_VIDEO3 <dmx_pes_type>`\:     fourth video PID.
     \* @:c:type:`DMX_PES_TELETEXT3 <dmx_pes_type>`\:  fourth teletext PID.
     \* @:c:type:`DMX_PES_SUBTITLE3 <dmx_pes_type>`\:  fourth subtitle PID.
     \* @:c:type:`DMX_PES_PCR3 <dmx_pes_type>`\:       fourth Program Clock Reference PID.
     \*
     \* @:c:type:`DMX_PES_OTHER <dmx_pes_type>`\:      any other PID.
     \*\/

    :c:type:`dmx_ts_pes <dmx_pes_type>` \{
            :c:type:`DMX_PES_AUDIO0 <dmx_pes_type>`,
            :c:type:`DMX_PES_VIDEO0 <dmx_pes_type>`,
            :c:type:`DMX_PES_TELETEXT0 <dmx_pes_type>`,
            :c:type:`DMX_PES_SUBTITLE0 <dmx_pes_type>`,
            :c:type:`DMX_PES_PCR0 <dmx_pes_type>`,

            :c:type:`DMX_PES_AUDIO1 <dmx_pes_type>`,
            :c:type:`DMX_PES_VIDEO1 <dmx_pes_type>`,
            :c:type:`DMX_PES_TELETEXT1 <dmx_pes_type>`,
            :c:type:`DMX_PES_SUBTITLE1 <dmx_pes_type>`,
            :c:type:`DMX_PES_PCR1 <dmx_pes_type>`,

            :c:type:`DMX_PES_AUDIO2 <dmx_pes_type>`,
            :c:type:`DMX_PES_VIDEO2 <dmx_pes_type>`,
            :c:type:`DMX_PES_TELETEXT2 <dmx_pes_type>`,
            :c:type:`DMX_PES_SUBTITLE2 <dmx_pes_type>`,
            :c:type:`DMX_PES_PCR2 <dmx_pes_type>`,

            :c:type:`DMX_PES_AUDIO3 <dmx_pes_type>`,
            :c:type:`DMX_PES_VIDEO3 <dmx_pes_type>`,
            :c:type:`DMX_PES_TELETEXT3 <dmx_pes_type>`,
            :c:type:`DMX_PES_SUBTITLE3 <dmx_pes_type>`,
            :c:type:`DMX_PES_PCR3 <dmx_pes_type>`,

            :c:type:`DMX_PES_OTHER <dmx_pes_type>`
    \};

    \#define DMX\_PES\_AUDIO    :c:type:`DMX_PES_AUDIO0 <dmx_pes_type>`
    \#define DMX\_PES\_VIDEO    :c:type:`DMX_PES_VIDEO0 <dmx_pes_type>`
    \#define DMX\_PES\_TELETEXT :c:type:`DMX_PES_TELETEXT0 <dmx_pes_type>`
    \#define DMX\_PES\_SUBTITLE :c:type:`DMX_PES_SUBTITLE0 <dmx_pes_type>`
    \#define DMX\_PES\_PCR      :c:type:`DMX_PES_PCR0 <dmx_pes_type>`

    \/\*\*
     \* struct :c:type:`dmx_filter` - Specifies a section header filter.
     \*
     \* @filter\: bit array with bits to be matched at the section header.
     \* @mask\: bits that are valid at the filter bit array.
     \* @mode\: mode of match\: if bit is zero, it will match if equal (positive
     \*        match); if bit is one, it will match if the bit is negated.
     \*
     \* Note\: All arrays in this struct have a size of DMX\_FILTER\_SIZE (16 bytes).
     \*\/
    struct :c:type:`dmx_filter` \{
            \_\_u8  filter[DMX\_FILTER\_SIZE];
            \_\_u8  mask[DMX\_FILTER\_SIZE];
            \_\_u8  mode[DMX\_FILTER\_SIZE];
    \};

    \/\*\*
     \* struct :c:type:`dmx_sct_filter_params` - Specifies a section filter.
     \*
     \* @pid\: PID to be filtered.
     \* @filter\: section header filter, as defined by \&struct dmx\_filter.
     \* @timeout\: maximum time to filter, in milliseconds.
     \* @flags\: extra flags for the section filter.
     \*
     \* Carries the configuration for a MPEG-TS section filter.
     \*
     \* The @flags can be\:
     \*
     \*      - \%DMX\_CHECK\_CRC - only deliver sections where the CRC check succeeded;
     \*      - \%DMX\_ONESHOT - disable the section filter after one section
     \*        has been delivered;
     \*      - \%DMX\_IMMEDIATE\_START - Start filter immediately without requiring a
     \*        \:ref\:\`DMX\_START\`.
     \*\/
    struct :c:type:`dmx_sct_filter_params` \{
            \_\_u16             pid;
            struct :c:type:`dmx_filter` filter;
            \_\_u32             timeout;
            \_\_u32             flags;
    \#define :c:type:`DMX_CHECK_CRC <dmx_sct_filter_params>`       1
    \#define :c:type:`DMX_ONESHOT <dmx_sct_filter_params>`         2
    \#define :c:type:`DMX_IMMEDIATE_START <dmx_sct_filter_params>` 4
    \};

    \/\*\*
     \* struct :c:type:`dmx_pes_filter_params` - Specifies Packetized Elementary Stream (PES)
     \*      filter parameters.
     \*
     \* @pid\:        PID to be filtered.
     \* @input\:      Demux input, as specified by \&enum dmx\_input.
     \* @output\:     Demux output, as specified by \&enum dmx\_output.
     \* @pes\_type\:   Type of the pes filter, as specified by \&enum dmx\_pes\_type.
     \* @flags\:      Demux PES flags.
     \*\/
    struct :c:type:`dmx_pes_filter_params` \{
            \_\_u16           pid;
            :c:type:`dmx_input <dmx_input>`  input;
            enum :c:type:`dmx_output` output;
            :c:type:`dmx_ts_pes <dmx_pes_type>` pes\_type;
            \_\_u32           flags;
    \};

    \/\*\*
     \* struct :c:type:`dmx_stc` - Stores System Time Counter (STC) information.
     \*
     \* @num\: input data\: number of the STC, from 0 to N.
     \* @base\: output\: divisor for STC to get 90 kHz clock.
     \* @stc\: output\: stc in @base \* 90 kHz units.
     \*\/
    struct :c:type:`dmx_stc` \{
            unsigned int num;
            unsigned int base;
            \_\_u64 stc;
    \};

    \#define \ :ref:`DMX_START <dmx_start>`                \_IO('o', 41)
    \#define \ :ref:`DMX_STOP <dmx_stop>`                 \_IO('o', 42)
    \#define \ :ref:`DMX_SET_FILTER <dmx_set_filter>`           \_IOW('o', 43, struct :c:type:`dmx_sct_filter_params`\ )
    \#define \ :ref:`DMX_SET_PES_FILTER <dmx_set_pes_filter>`       \_IOW('o', 44, struct :c:type:`dmx_pes_filter_params`\ )
    \#define \ :ref:`DMX_SET_BUFFER_SIZE <dmx_set_buffer_size>`      \_IO('o', 45)
    \#define \ :ref:`DMX_GET_PES_PIDS <dmx_get_pes_pids>`         \_IOR('o', 47, \_\_u16[5])
    \#define \ :ref:`DMX_GET_STC <dmx_get_stc>`              \_IOWR('o', 50, struct :c:type:`dmx_stc`\ )
    \#define \ :ref:`DMX_ADD_PID <dmx_add_pid>`              \_IOW('o', 51, \_\_u16)
    \#define \ :ref:`DMX_REMOVE_PID <dmx_remove_pid>`           \_IOW('o', 52, \_\_u16)

    \#if !defined(\_\_KERNEL\_\_)

    \/\* This is needed for legacy userspace support \*\/
    typedef enum :c:type:`dmx_output` \ :c:type:`dmx_output_t <dmx_output>`\ ;
    typedef :c:type:`dmx_input <dmx_input>` :c:type:`dmx_input_t <dmx_input>`;
    typedef :c:type:`dmx_ts_pes <dmx_pes_type>` :c:type:`dmx_pes_type_t <dmx_pes_type>`;
    typedef struct :c:type:`dmx_filter` :c:type:`dmx_filter_t <dmx_filter>`;

    \#endif

    \#endif \/\* \_UAPI\_DVBDMX\_H\_ \*\/
