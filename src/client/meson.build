#  OpenVPN 3 Linux - Next generation OpenVPN
#
#  SPDX-License-Identifier: AGPL-3.0-only
#
#  Copyright (C)  OpenVPN Inc <sales@openvpn.net>
#  Copyright (C)  David Sommerseth <davids@openvpn.net>


#  openvpn3-service-backendstart
bin_backend_start = executable(
    'openvpn3-service-backendstart-dev',
    [
        'openvpn3-service-backendstart.cpp',
    ],
    include_directories: [include_dirs, '../..'],
    dependencies: [
        base_dependencies,
    ],
    link_with: [
        common_code
    ],
    install: true,
    install_dir: libexec_dir
)
# D-Bus policy
configure_file(
    input: '../policy/net.openvpn.v3.backends.conf.in',
    output: 'net.openvpn.v3.backends.conf',
    configuration: configuration_data(dbus_config),
    install: true,
    install_dir: dbus_policy_dir,
)
# D-Bus service autostart config
configure_file(
    input: '../service-autostart/template.service.in',
    output: 'net.openvpn.v3.backends.service',
    configuration: configuration_data(
        dbus_config +
        {
            'BUSNAME': 'net.openvpn.v3.backends',
            'SERVICE_BIN': bin_backend_start.name(),
            'SERVICE_ARGS': '',
        }
    ),
    install: true,
    install_dir: dbus_service_dir,
)