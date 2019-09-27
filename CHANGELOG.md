# Changelog
All notable changes to this project will be documented in this file.

## [0.2.1] - 2019-09-27
### Added
 - Tag `ntp_install`.
 - Tag `ntp_service`.
 - Install Packed `python-apt` for debian famili

### Changed
 - Variable rename from `service_is` to `ntp_service_is` 
 - Variable rename form `when_boot` to ntp_when_boot`
 - The code responsible for services has been moved to the main.yml file.

## [0.2.0] - 2019-04-31
### Added
 - Service configurations.

## [0.1.1] - 2019-04-15
### Added
 - The possibility of installing a role by Ansible Galaxy repositories.


## [0.1.0] - 2019-03-31
### Added
 - The main role for installing an NTP client.

[0.2.1]: https://github.com/KarolCode/Ansible-Role-NTP/compare/v0.2.0...v0.2.1
[0.2.0]: https://github.com/KarolCode/Ansible-Role-NTP/compare/v0.1.1...v0.2.0
[0.1.1]: https://github.com/KarolCode/Ansible-Role-NTP/compare/v0.1.0...v0.1.1
[0.1.0]: https://github.com/KarolCode/Ansible-Role-NTP/releases/tag/v0.1.0
