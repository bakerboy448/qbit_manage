# qbit_manage Run Commands

|            **Shell Command**            | **Docker Environment Variable** |   **Config Command**  | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                            | **Default Value** |
|:---------------------------------------:|:-------------------------------:|:---------------------:|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------:|
|              `-r` or`--run`             |             QBT_RUN             |           N/A         | Run without the scheduler. Script will exit after completion.                                                                                                                                                                                                                                                                                                                                                                                              |       False       |
|          `-sch` or `--schedule`         |           QBT_SCHEDULE          |           N/A         | Schedule to run every x minutes or choose customize schedule via [cron](https://crontab.guru/examples.html). (Default set to 1440 (1 day))                                                                                                                                                                                                                                                                                                                                                                                             |        1440       |
|        `-sd` or `--startup-delay`       |        QBT_STARTUP_DELAY        |           N/A         | Set delay in seconds on the first run of a schedule (Default set to 0)                                                                                                                                                                                                                                                                                                                                                                                     |         0         |
|  `-c CONFIG` or `--config-file CONFIG`  |            QBT_CONFIG           |           N/A         | This is used if you want to use a different name for your config.yml. `Example: tv.yml`                                                                                                                                                                                                                                                                                                                                                                    |     config.yml    |
| `-lf LOGFILE,` or `--log-file LOGFILE,` |           QBT_LOGFILE           |           N/A         | This is used if you want to use a different name for your log file. `Example: tv.log`                                                                                                                                                                                                                                                                                                                                                                      |    activity.log   |
|         `-cs` or `--cross-seed`         |          QBT_CROSS_SEED         |       cross_seed      | Use this after running [cross-seed script](https://github.com/mmgoodnow/cross-seed) to add torrents from the cross-seed output folder to qBittorrent                                                                                                                                                                                                                                                                                                       |       False       |
|           `-re` or `--recheck`          |           QBT_RECHECK           |         recheck       | Recheck paused torrents sorted by lowest size. Resume if Completed.                                                                                                                                                                                                                                                                                                                                                                                        |       False       |
|         `-cu` or `--cat-update`         |          QBT_CAT_UPDATE         |       cat_update      | Use this if you would like to update your categories or move from one category to another.                                                                                                                                                                                                                                                                                                                                                                 |       False       |
|         `-tu` or `--tag-update`         |          QBT_TAG_UPDATE         |       tag_update      | Use this if you would like to update your tags and/or set seed goals/limit upload speed by tag. (Only adds tags to untagged torrents)                                                                                                                                                                                                                                                                                                                      |       False       |
|      `-ru` or `--rem-unregistered`      |       QBT_REM_UNREGISTERED      |    rem_unregistered   | Use this if you would like to remove unregistered torrents. (It will the delete data & torrent if it is not being cross-seeded, otherwise it will just remove the torrent without deleting data). Trackers that have an error and not covered by the remove unregistered logic will also be tagged as `issue` for manual review.                                                                                                                           |       False       |
|     `-tte` or `--tag-tracker-error`     |      QBT_TAG_TRACKER_ERROR      |    tag_tracker_error  | Use this if you would like to tag torrents that do not have a working tracker.                                                                                                                                                                                                                                                                                                                                                                             |       False       |
|        `-ro` or `--rem-orphaned`        |         QBT_REM_ORPHANED        |      rem_orphaned     | Use this if you would like to remove orphaned files from your `root_dir` directory that are not referenced by any torrents. It will scan your `root_dir` directory and compare it with what is in qBittorrent. Any data not referenced in qBittorrent will be moved into `/data/torrents/orphaned_data` folder for you to review/delete.                                                                                                                   |       False       |
|      `-tnhl` or `--tag-nohardlinks`     |       QBT_TAG_NOHARDLINKS       |     tag_nohardlinks   | Use this to tag any torrents that do not have any hard links associated with any of the files. This is useful for those that use Sonarr/Radarr that hard links your media files with the torrents for seeding. When files get upgraded they no longer become linked with your media therefore will be tagged with a new tag noHL. You can then safely delete/remove these torrents to free up any extra space that is not being used by your media folder. |       False       |
|        `-sl` or `--share-limits`        |         QBT_SHARE_LIMITS        |      share_limits     | Control how torrent share limits are set depending on the priority of your grouping. Each torrent will be matched with the share limit group with the highest priority that meets the group filter criteria. Each torrent can only be matched with one share limit group.                                                                                                                                                                                  |       False       |
|        `-sc` or `--skip-cleanup`        |         QBT_SKIP_CLEANUP        |      skip_cleanup     | Use this to skip emptying the Recycle Bin folder (`/root_dir/.RecycleBin`) and Orphaned directory. (`/root_dir/orphaned_data`)                                                                                                                                                                                                                                                                                                                             |       False       |
|           `-dr` or `--dry-run`          |           QBT_DRY_RUN           |         dry_run       | If you would like to see what is gonna happen but not actually move/delete or tag/categorize anything.                                                                                                                                                                                                                                                                                                                                                     |       False       |
|     `-ll` or `--log-level LOGLEVEL`     |          QBT_LOG_LEVEL          |           N/A         | Change the output log level.                                                                                                                                                                                                                                                                                                                                                                                                                               |        INFO       |
|                `--debug`                |            QBT_DEBUG            |           N/A         | Adds debug logs                                                                                                                                                                                                                                                                                                                                                                                                                                            |       False       |
|                `--trace`                |            QBT_TRACE            |           N/A         | Adds trace logs                                                                                                                                                                                                                                                                                                                                                                                                                                            |       False       |
|           `-d` or `--divider`           |           QBT_DIVIDER           |           N/A         | Character that divides the sections (Default: '=')                                                                                                                                                                                                                                                                                                                                                                                                         |         =         |
|            `-w` or `--width`            |            QBT_WIDTH            |           N/A         | Screen Width (Default: 100)                                                                                                                                                                                                                                                                                                                                                                                                                                |        100        |
|   `-svc` or `--skip-qb-version-check`   |    QBT_SKIP_QB_VERSION_CHECK    | skip_qb_version_check | Bypass qBittorrent/libtorrent version compatibility check. You run the risk of undesirable behavior and WILL RECIEVE NO SUPPORT.                                                                                                                                                                                                                                                                                                                           |       False       |