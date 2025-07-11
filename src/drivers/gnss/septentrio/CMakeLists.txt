############################################################################
#
#   Copyright (c) 2024 PX4 Development Team. All rights reserved.
#
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions
# are met:
#
# 1. Redistributions of source code must retain the above copyright
#    notice, this list of conditions and the following disclaimer.
# 2. Redistributions in binary form must reproduce the above copyright
#    notice, this list of conditions and the following disclaimer in
#    the documentation and/or other materials provided with the
#    distribution.
# 3. Neither the name PX4 nor the names of its contributors may be
#    used to endorse or promote products derived from this software
#    without specific prior written permission.
#
# THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
# "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
# LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS
# FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE
# COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT,
# INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING,
# BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS
# OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED
# AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT
# LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN
# ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE
# POSSIBILITY OF SUCH DAMAGE.
#
############################################################################

px4_add_module(
	MODULE driver__septentrio
	MAIN septentrio
	COMPILE_FLAGS
		# -DDEBUG_BUILD           # Enable during development of the module
		-DSEP_LOG_ERROR         # Enable module-level error logs
		# -DSEP_LOG_WARN          # Enable module-level warning logs
		# -DSEP_LOG_INFO          # Enable module-level info logs
		# -DSEP_LOG_TRACE_PARSING # Tracing of parsing steps
	SRCS
		septentrio.cpp
		util.cpp
		rtcm.cpp
		sbf/decoder.cpp
	MODULE_CONFIG
		module.yaml
	)

px4_add_functional_gtest(SRC septentrio_fuzz_tests.cpp
	LINKLIBS
		driver__septentrio
	COMPILE_FLAGS
		# There warnings come from within fuzztest
		-Wno-float-equal
		-Wno-sign-compare
		-Wno-shadow
		-Wno-extra
		-Wno-non-template-friend
)
