# Redmine Time Tracker plugin for Redmine >= 3.0

Time tracker is a Redmine plugin to ease time tracking when working on an issue.
The plugin allows to start/suspend/resume/stop a timer on a per user basis.

## Features

* Current spent time always visible
* Timer automatic updated without reload
* Per user time tracking
* Using known 'log time' dialog

## Install

1. Follow the [Redmine plugin installation](http://www.redmine.org/wiki/redmine/Plugins) steps. Make sure the plugin is installed to `plugins/redmine_time_tracker`
2. Setup the database using the migrations `rake redmine:plugins:migrate RAILS_ENV=production`
3. Login to your Redmine install as an Administrator
4. Setup the "log time" permissions for your roles
5. Add "Time tracking" to the enabled modules for your project
6. The link to the plugin should appear in the 'account' menu bar

## Uninstall

1. Run `rake redmine:plugins:migrate NAME=redmine_time_tracker VERSION=0 RAILS_ENV=production`
2. Delete folder `<redmine_root>/plugins/redmine_time_tracker`

## Usage

To be able to use a time tracker, a user must have the 'log time' permission. Then, the current time tracker information are displayed in the top right menu, next to the user info.

These information are context dependant:

- If the user does not have a running time tracker yet, a message telling so will be displayed.
- If the user does not have a running time tracker yet but he is displaying an issue, then the 'start' action will be displayed.
- If the user has a running time tracker, the current spent time is displayed (and refreshed periodically) next to the tracked issue number. The 'pause' or the 'resume' action will be displayed as well as the 'stop' one too. Stopping the time tracker will redirect the user to the standard time logging page with the 'hours' field filled with the time tracker value. This way, we rely on existing and well known behaviours.

To be noted that these actions are available in the issues list context menu too (right click in the issues list).

A 'list' action is displayed in the menu too. This action will redirect the user to a page listing his time tracker and other user's ones if the 'view others time trackers' right is set. From this list, the user can 'delete' his time tracker (or the other user's ones if the 'delete others time trackers' permission is set).

The plugin settings page allows to define the spent time refresh rate, redirect after stopping and the status transition to apply when a time tracker is started. For example, if a transition 'New' -> 'In progress' is added, starting a time tracker on an issue having the 'New' status will automatically change it to 'In progress'.
