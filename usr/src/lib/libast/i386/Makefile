#
# CDDL HEADER START
#
# The contents of this file are subject to the terms of the
# Common Development and Distribution License (the "License").
# You may not use this file except in compliance with the License.
#
# You can obtain a copy of the license at usr/src/OPENSOLARIS.LICENSE
# or http://www.opensolaris.org/os/licensing.
# See the License for the specific language governing permissions
# and limitations under the License.
#
# When distributing Covered Code, include this CDDL HEADER in each
# file and include the License file at usr/src/OPENSOLARIS.LICENSE.
# If applicable, add the following below this CDDL HEADER, with the
# fields enclosed by brackets "[]" replaced with your own identifying
# information: Portions Copyright [yyyy] [name of copyright owner]
#
# CDDL HEADER END
#

#
# Copyright 2008 Sun Microsystems, Inc.  All rights reserved.
# Use is subject to license terms.
#

# Platform-specific config
# Note that "HOSTTYPE" matches the value used by AT&T upstream.
ASTPLATFORMCPPFLAGS = '-DHOSTTYPE="sol$(RELEASE_MINOR).i386"'

# platform-specific sources
OBJECTS = \
	i386/src/lib/libast/conftab.o \
	i386/src/lib/libast/lctab.o
OBJDIRS = \
	i386/src/lib/libast

include ../Makefile.com

# Use big PIC since libast is too big for pic on 64bit
# (and on 32bit it is close to the barrier)
i386_C_PICFLAGS  = $(C_BIGPICFLAGS)

install: all $(ROOTLIBS) $(ROOTLINKS)
