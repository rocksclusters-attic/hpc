#
# $Id: Makefile,v 1.18 2012/11/27 00:49:01 phil Exp $
#
# @Copyright@
# 
# 				Rocks(r)
# 		         www.rocksclusters.org
# 		         version 5.6 (Emerald Boa)
# 		         version 6.1 (Emerald Boa)
# 
# Copyright (c) 2000 - 2013 The Regents of the University of California.
# All rights reserved.	
# 
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions are
# met:
# 
# 1. Redistributions of source code must retain the above copyright
# notice, this list of conditions and the following disclaimer.
# 
# 2. Redistributions in binary form must reproduce the above copyright
# notice unmodified and in its entirety, this list of conditions and the
# following disclaimer in the documentation and/or other materials provided 
# with the distribution.
# 
# 3. All advertising and press materials, printed or electronic, mentioning
# features or use of this software must display the following acknowledgement: 
# 
# 	"This product includes software developed by the Rocks(r)
# 	Cluster Group at the San Diego Supercomputer Center at the
# 	University of California, San Diego and its contributors."
# 
# 4. Except as permitted for the purposes of acknowledgment in paragraph 3,
# neither the name or logo of this software nor the names of its
# authors may be used to endorse or promote products derived from this
# software without specific prior written permission.  The name of the
# software includes the following terms, and any derivatives thereof:
# "Rocks", "Rocks Clusters", and "Avalanche Installer".  For licensing of 
# the associated name, interested parties should contact Technology 
# Transfer & Intellectual Property Services, University of California, 
# San Diego, 9500 Gilman Drive, Mail Code 0910, La Jolla, CA 92093-0910, 
# Ph: (858) 534-5815, FAX: (858) 534-7345, E-MAIL:invent@ucsd.edu
# 
# THIS SOFTWARE IS PROVIDED BY THE REGENTS AND CONTRIBUTORS ``AS IS''
# AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO,
# THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
# PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE REGENTS OR CONTRIBUTORS
# BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
# CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
# SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR
# BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY,
# WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE
# OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN
# IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
# 
# @Copyright@
#
#
# $Log: Makefile,v $
# Revision 1.18  2012/11/27 00:49:01  phil
# Copyright Storm for Emerald Boa
#
# Revision 1.17  2012/09/30 21:58:56  phil
# Update openmpi to 1.6.2.
# Create Modules for ethernet and IB
# Add IB support - packages, openmpi configuration, udev rules
#
# Revision 1.16  2012/05/06 05:49:10  phil
# Copyright Storm for Mamba
#
# Revision 1.15  2012/04/06 19:49:49  phil
# environment modules file
#
# Revision 1.14  2011/10/07 18:52:00  anoop
# Bug fix
#
# Revision 1.13  2011/07/23 02:31:05  phil
# Viper Copyright
#
# Revision 1.12  2010/09/07 23:53:20  bruno
# star power for gb
#
# Revision 1.11  2010/03/08 04:36:50  anoop
# Upgraded OpenMPI to 1.4.1
# Added mpi-selector capability
#
# Revision 1.10  2009/05/01 19:07:18  mjk
# chimi con queso
#
# Revision 1.9  2008/10/18 00:56:10  mjk
# copyright 5.1
#
# Revision 1.8  2008/10/15 20:13:04  mjk
# - more changes to build outside of the tree
# - removed some old fds-only targets
#
# Revision 1.7  2008/04/07 23:03:02  bruno
# add openmpi back into HPC roll. the bio roll will use thie mpi environment
# to for a couple of its apps.
#
#

PKGROOT = /opt/openmpi
REDHAT.ROOT = $(CURDIR)/../../

-include $(ROCKSROOT)/etc/Rules.mk
include Rules.mk

%: %.in
	$(SED) $(SEDSCRIPT) $^ > $@

build:
	bunzip2 -c openmpi-$(VERSION).tar.bz2 | $(TAR) -xf -
	(					\
		cd openmpi-$(VERSION) ;		\
		./configure --prefix=$(PKGROOT) \
			--with-openib --with-udapl \
			--with-sge \
			--enable-static ;	\
		$(MAKE) all ;			\
	)

install:: 
	(					\
		cd openmpi-$(VERSION) ;		\
		$(MAKE) prefix=$(ROOT)/$(PKGROOT) install ;	\
	)
	( find mpi-selector -type f | grep -v CVS | \
		cpio -pudv $(ROOT)/$(PKGROOT)/share/ )

clean::
	rm -rf openmpi-$(VERSION)
	rm -rf $(NAME).spec.in


