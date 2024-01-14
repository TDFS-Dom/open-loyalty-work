# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/)
and this project adheres to [Semantic Versioning](http://semver.org/spec/v2.0.0.html).

## [3.1.0] - 14-01-2019

Note! In this version introduced a few features that breaks backward-compatibility.
Note2! Check UPGRADE-3.1.md to see how to upgrade.

### Added
- Added Snapshots for Event Sourcing to increase performance
- Added new options for expiring points in Settings -> Configuration (all time active / after x number of days / at the end of the month / at the end of the year) (new feature)
- Added User Guide at https://open-loyalty.readthedocs.io
- Added new ACL for administration panel (new feature) (BC break)
- Added return "Voucher" for a customer during registration a return transaction (new feature)
- Added information about active and used points to the export in levels
- GET /api/admin/customer/{customerId}/status added information about points going to expire in next month
- GET /api/seller/customer/{customerId}/status added information about points going to expire in next month
- GET /api/customer/{customerId}/status added information about points going to expire in next month
- Added option "Fulfillment Tracking Process" to the Reward Campaign so an administration is able to change reward status (ordered / delivered / canceled / shipped) (new feature)
- Added usage datetime of coupon in the GET /api/campaign/bought
- Added an option at Settings -> Configuration to disable edit customer profile by himself except password change (new feature)
- Added new filters "isFeatured", "hasSegment", "categoryId[]", "format" to GET /api/campaign/public/available
- Added an integration with Pushy to send push notifications (new feature)
- Added missing configuration to notify a customer a X number of days before level expires using Webhooks
- GET /api/admin/customer/{customerId}/status added information about points expiration per day
- GET /api/seller/customer/{customerId}/status added information about points expiration per day
- GET /api/customer/{customerId}/status added information about points points expiration per day
- Added limitation by POS, segments and levels in the Earning Rule with type "Geolocation"
- Added sending information about rewards that became available for a customer using push notifications (new feature)
- Added new types of "Usage limit active" for "Custom event rule" in Earning rule
- Added an configuration (simple/advanced) in the app/config/parameters.yml to change password requirements
- Added an configuration in the app/config/parameters.yml to change the length of activation code sent using SMS activation method
- Added upload avatar for a customer profile (new feature)
- Added support for IE 11 for an administration panel
- Added POST /api/customer/earnRule/{eventName} to call "Custom event" Earning Rule with customer JWT Token
- Added migration mechanism using Doctrine Migrations (new feature)

### Changed
- Prevent from registering a return transaction for non-existing transaction by documentNumber field
- Prevent marking coupon as Unused by a customer
- Changed Nginx version to 1.14.1 
- PUT /api/customer/{customer} works now as a partial update instead of full update (BC break)
- Earning Rule with type "Geolocation" accepts now coordinates with five digits after decimal point
- Increased php-fpm start processes to 5, min processes to 3 and max processes to 20
- Increased php-fpm memory limit to 512MB
- PHP-FPM is now configurable using docker/prod/php/conf/php-fpm-pool.conf
- Changed translation in Settings - Notify user from "Days to level recalculation" to "Days before level recalculation to notify user"
- Updated the documentation how to add a new segment
- Disabled remove already redeemed coupons by a customer from Reward Campaign
- Renamed GET /api/campaign/public/featured to GET /api/campaign/public/available
- Removed filter "isPublic" from GET /api/campaign/public/available
- Changed how projections to the Elasticsearch works by making them independent of each other
- Changed ol__setings table by adding a unique constraint for setting_key column
- Changed invitation process when SMS activation method is enabled POST /api/invitations/invite (BC break)
- Changed crons by adding flock
- Changed default sorting to "order" for categories of Reward Campaign in the administration panel
- Removed "program_name" parameter from app/config/parameters.yml

### Fixed
- Fixed calling API endpoints starting with /api/customer by an administrator using X-AUTH-TOKEN
- Fixed marking coupon as Used / Unused by an administrator
- Fixed calculating level based on "Active points"
- Fixed calculating level based on "Total points earned since last level recalculation"
- Fixed automatically assign a birth date to the customer during update
- Fixed PUT /api/customer/{customer} so it won't remove labels accidentally
- Fixed translate level name on GET /api/customer/status?_locale={locale} according to the locale passed in the query parameter
- Fixed 500 error while registering a new transaction when at least one Earning Rule has set option "All time active"
- Fixed that an administrator see only "Example_coupon" on the Reward Campaign's edit page
- Fixed adding points manually so it now has an impact on customer level
- Fixed 500 error when now level with condition value equal zero is defined
- Fixed activating and expiring coupons
- Fixed 500 error during creating Reward Campaign with type "Instant Reward"
- Fixed removing a language from the configuration
- Fixed logo size on the administration panel sites
- Fixed adding a new customer by an administrator in specific system configuration
- Fixed using Earning Rule with type "QR code"
- Fixed changing type of Earning Rule during creating a new one
- Fixed forgot password when customers phone number was changed
- Fixed usageLeftForCustomer value in GET /api/customer/campaign/available for single coupon
- Fixed filtering by date in redeemed rewards table
- Fixed remove field value while edit Reward Campaign in the administration panel
- Fixed sorting GET /api/admin/customer/{customer}/campaign/available using sort=campaignVisibility.visibleFrom
- Fixed GET /admin/analytics/points to show a correct number of spent points in loyalty program
- Fixed 500 error while buy reward campaign in POST /api/admin/customer/{customer}/campaign/{campaign}/buy
- Fixed crons for expire or activate coupons
- Fixed 500 error when a transaction missed a required documentNumber field POST /api/transaction
- Fixed supervisord in the production docker image
- Fixed edit customer profile automatically set a manual level and disabled level change
- Fixed selectbox shows only 10 segments while create Reward Campaign or Earning Rule
- Fixed missing markdown for shortDescription in the Reward Campaign
- Fixed unable to extend section with default language
- Fixed showing a customer in the more than one level list at the same time GET /api/level/{levelId}/customers
- Fixed import transaction using the same documentNumber more then once
- Fixed mark coupon as used by an administrator POST /api/admin/campaign/coupons/mark_as_used (BC break)
- Fixed 500 error while import transactions without or with invalid posId
- Fixed Earning Rule with type "Account created" that was never called
- Fixed "Timezone" setting at Settings -> Configuration
- Fixed value of "usageLeftForCustomer" in GET /api/customer/campaign/available when single coupon used

## [3.0.0] - 15-10-2018

### Added
- multi photos for reward campaigns (new feature)
- segments, levels and POS limits now available in the Geolocation Earning Rule (new feature)
- Custom Reward Campaign that allows to link with Custom Earning Rule or QRCode Earning rule and reward customer with points (new feature)
- QRCode Earning Rule (new feature)
- new currency HDK to the settings
- multi language for Levels, Reward Campaigns, Reward Campaigns Category (new feature)
- new API endpoint /api/settings/css allowing to get custom CSS rules for Client Cockpit
### Changed
- importing transaction with POS information is now simplified, you can define posIdentifier or posId
- size of textareas has been decreased
### Fixed
- data in Elastic Search was not always up to date
- unable to add a points transfer when customer databases was large
- a phone number was not copied from customer to transaction while matching transaction with customer
- customer could register twice with the same phone number when activation method is SMS
- a negative radius value in Geolocation Earning Rule caused 500 error
- while creating Reward Campaign there was only first 10 reward categories to choose, now unlimited
- buying a campaign when a customer has no phone number caused 500 error
- fixed typos
- missing translations

## [2.10.0] - 24-09-2018

### Added
- your points will expire soon (web hook)
- you level will expire soon (web hook)
- new level calculation mode
- information about bought products in transfer points to avoid uneccesary calls
- new logos in Settings -> Configuration
- polish translation for backend validation
- generating a manifest file from Settings -> Configuration
- new web hook when a customer has been deactivated
- added level name to the onCustomerLevelChangedAutomatically (web hook)
- filter to /api/points/transfer to filter only active and expired points
- filter to /api/points/transfer to filter points by expiration date
- points transfer between customers (new feature)
- brand icon for Reward Campaigns
- categories for Reward Campaigns (new feature)
- a new flag, feature for Reward Campaigns
- coupon expiration (new feature)
- your points will expire soon (web hook)
- Earning Rule based on customer localization (new feature)
- information how many points you need to earn to stay in the same level
- added flag "public" to the Reward Campaign
- buying many coupons at once (new feature)
- an administrator can buy a campaign as a customer with or without using customer points (new feature)
- resetting level after a certain time (new feature)
- cancel coupon when a transaction has been fully returned (new feature)
- using many coupons at once (new feature)
- custom static segments (new feature)
### Changed
- import transfer points using customer email/phone number/loyalty card number
- PUT /api/customer/{customer} is now a partial update, not full update
- increased max_result_window for Elasticsearch to return more documents
- removed column with template name from CSettings -> Emails table
- removed redundant web hook onCustomerLevelChanged
- logic how a customer will be downgraded or upgraded to next level
- searching customers in POS by name or last name as a wildcard
### Fixed
- added missing translations
- phone number validation (less restrict)
- creating a new earning rule after changing it's type
- matching transaction with customer using upper letters
- table pagination
- creating a reward campaign other than Cash Back
- assign a new percent discount code to the customer

## [2.9.0] - 20-08-2018
### Added
- configurable e-mail content for referring a friend
- markdown for campaign details
- new earning rule "Instant Reward" to collect rewards instantly after a transaction
- include/exclude labels for earning rule "General Spending Rule"
- locking points for X number of days
- assign earning rules to the POS
- set earning rule as last
### Changed
- label value for the customer is not required anymore
### Fixed
- download level list as CSV file
- translations
- search client by first or last name in POS
- upload button in firefox
- upgrading read model
- dashboard
- points transfer list in client cockpit
- creating Earning Rule without labels

## [2.8.0] - 20-07-2018
### Added
- configuring marketing automation tool in the administration panel
- new command "phing migrate" to automate migration between versions
- new development documentation
- master key API token
- filtering campaign through additional fields
- seller can add or spend points for a customer
- assign earning rule to the POS
- resizing logos
- added level ID to the endpoint /api/customer/level
### Changed
- changed Earning Points Rules to Earning Rules
### Fixed
- validation tags on Earning Rule "Multiply by labels"
- fixed link to the terms and conditions file
- fixed bug with Earning Rule "Custom event rule"
- generating demo data

## [2.7.0] - 03-07-2018
### Added
- possibility to set an accent color for client cockpit
- /api/customer/level to get list of possible levels for customers
- added new earning points rule "Multiply by product label"
- new configuration option to upload terms and condition file
- labels to the transaction
- labels to the reward campaigns
### Changed
- docker images
- docker-compose settings, check updated README.md
### Fixed
 - sorting for /api/customer/campaign/available
 - registering a refund transaction and subtracting points
 - saving settings with a various set of values
 - changing reward campaign photo
 - forgot password on client cockpit

## [2.6.0] - 05-06-2018
### Added
- upload customer from XML file
- add Earning Points Rule name to the Transfer Points comment (https://github.com/DivanteLtd/open-loyalty/issues/79)
### Changed
- segment or level is now required in Earning Points Rules
- only png/jpg/jpeg files are now supported for logo
- updated Symfony to latest version 3.4.11 with security fixes
### Fixed
- generating demo data
- updating administrator account
- choosing different language in Settings -> Configuration (https://github.com/DivanteLtd/open-loyalty/issues/83)

## [2.5.0] - 25-05-2018
### Added
- added property hasPhoto to indicate a model has photo in campaigns, earning points rules and levels
- added photo to Levels
- added photo to Earning Points Rules
- added uploading transactions from XML file
- added new Reward Campaign "CashBack"
- added a new property "Prize value" to the Reward Campaigns
- added a new property "Tax" to the Reward Campaigns
- added a new settings "Small logo"
- added uploading points transfers from XML file
- added a new sorting filter "manuallyAssignedLevel" to the customer list
- added a method to unassign a customer from assigned manually level /api/customer/{customer}/remove-manually-level
### Changed
- upgraded minimum version of PHP from 7.0 to 7.1
- changed campaignId object to string in response from /api/customer/campaign/bought
- property "pointsEarned" is now always available in the /api/transaction response

## [2.4.0] - 23-04-2018
### Added
- added missing translations
- added translatable program name in the title bar in browser
- added list of redeemed rewards
- added matching transaction with a customer using phone number
- added new SMS gateway WorldText
- added possibility to log in using phone number
- added settings to change activation method (e-mail or sms)
- added endpoint to match transactions by a customer
### Fixed
- fixed minor bugs with customer activation using SMS
- fixed searching customers (/api/customer)

## [2.3.1] - 12-04-2018
### Added
- added [API documentation](http://open-loyalty.readthedocs.io/en/latest/)

## [2.3.0] - 05-04-2018
### Added
- added API aliases to fix X-AUTH-TOKEN invalid credentials
- added comment to the points transfer list
- added missing translations
- added a new feature to activate a customer using SMS
### Fixed
- fixed SQL Injection vulnerabilities

## [2.2.0] - 28-02-2018
### Added
- encryption parameter for swiftmailer
- logo validation
- added APCu cache layer for mappings and query building in Doctrine ORM
- better concurrency support for writings
- increased performance
- added makefile for common used commands
### Changed
- upgraded jquery to 3.x version to fix potential vulnerabilities
- upgraded Symfony framework to version 3.4 LTS
- upgraded Broadway library to version 2.0.1 (it's a BC break)
- changed README.md
### Fixed
- changing merchant data in AC
- searching a client in POSC
- rounding points in emails

## [2.1.0] - 28-01-2018
### Added
- Added new customer account statuses (it's a BC break!)
- Collect / spend points only when a customer has a defined status
- Support GDPR
- A new setting where you can change loyalty program logo
- More information link field for a reward campaign
- Display reward campaing's image in client cockpit
### Fixed
- Missing transactions in the POS cockpit
- Remove transfer points in Admin Cockpit
- Vagrant setup for Windows users
- Fixes missing placeholders

## [2.0.0] - 2017-11-016
### Added
- Kubernetes support
### Changed
- Docker files
- Frontend migration from Gulp to the Webpack
- Migration from Nodejs server to the Nginx

## [1.4.0] - 2017-11-07
### Added
- CLI command to restore read model using event store
### Fixed
- AC/POSC fixed transaction id
- AC/POSC show points for each transaction
- AC clear fields after changing event type
- POSC fixed missing days from last order
- CC fixed cancel button

## [1.3.1] - 2017-10-23
### Added
- Added change log file
### Changed
- API Documentation
- Changed guide link in the admin cockpit
### Fixed
- Reload application after language change
- Fixed renaming translation name

## [1.3.0] - 2017-10-09
### Changed
- Added new endpoints to the API documentation
### Fixed
- Fixed PHPUnit configuration
- Changed label for Postgres from latest to version 9

## [1.2.1] - 2017-09-28
### Added
- Added API documentation
### Fixed
- Fixed wrong marketing agreement label
- Fixed table width on the transaction details
- View level & segment names instead of ID in the reward campaign view
- Show newly added language in the settings

## [1.2.0] - 2017-09-08
### Changed
- Moved code to the vendor
### Fixed
- Fixed customer activation link
- Fixed variables in the e-mail templates
- Fixed link to the page "See rewards you have already redeemed"

## [1.1.0] - 2017-07-21
### Changed
- Allow decimal numbers for point value field in the general spending rule
- Change default language from PL to EN
### Fixed
- Fixed loader look
