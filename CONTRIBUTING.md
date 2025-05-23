# Contributing Guide

- [How to?](#how-to)
- [Data Scheme](#data-scheme)
- [Channel Logo Guidelines](#channel-logo-guidelines)
- [Project Structure](#project-structure)
- [Scripts](#scripts)
- [Workflows](#workflows)

## How to?

### How to add a new channel to the database?

The easiest way is to send a request through this [form](https://github.com/iptv-org/database/issues/new?assignees=&labels=channels%3Aadd&projects=&template=1_channels_add.yml&title=Add%3A+). Just fill in all the information you know about the channel and press send. Once your request is approved, the channel will automatically be added to the database.

If you want to add more than one channel, you can do it directly by editing the [data/channels.csv](data/channels.csv) file in any text editor. After that, just [commit](https://docs.github.com/en/pull-requests/committing-changes-to-your-project/creating-and-editing-commits/about-commits) all changes and send us a [pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests).

**IMPORTANT:** Before sending the request, make sure that the number of columns in the file has not changed and that all rows end with [CRLF](https://developer.mozilla.org/en-US/docs/Glossary/CRLF). Otherwise we will not be able to review this request.

### How to edit channel description?

As with adding a channel, this can be done in several ways.

The first option is to send a request through this [form](https://github.com/iptv-org/database/issues/new?assignees=&labels=channels%3Aedit&projects=&template=2_channels_edit.yml&title=Edit%3A+). Just specify the ID of the channel you want to edit and the new data. To delete a value, insert `~` in the desired field. After your request is approved, the channel description will be automatically updated.

The second option is to edit the [data/channels.csv](data/channels.csv) file using a text editor and then send us a [pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests).

**IMPORTANT:** Before sending the request, make sure that the number of columns in the file has not changed and that all rows end with [CRLF](https://developer.mozilla.org/en-US/docs/Glossary/CRLF). Otherwise we will not be able to review this request.

### How to remove a channel from the database?

To remove a channel fill out this [form](https://github.com/iptv-org/database/issues/new?assignees=&labels=channels%3Aremove&projects=&template=3_channels_remove.yml&title=Remove%3A+) with channel ID and the reason for deletion.

**NOTE:** Closing a channel is not a reason to remove it from the database.

### How to mark a channel as closed?

To do this, use this [form](https://github.com/iptv-org/database/issues/new?assignees=&labels=channels%3Aedit&projects=&template=2_channels_edit.yml&title=Edit%3A+). In it, in the "Closed" field you will need to specify at least the approximate date of closing. And there you can also specify the ID of the channel that replaced it, if necessary.

### How to add a new feed to the database?

_Option 1:_ Send a request through this [form](https://github.com/iptv-org/database/issues/new?assignees=&labels=feeds%3Aadd&projects=&template=4_feeds_add.yml&title=Add%3A+). Fill in all the information you know about the feed and press send. Once your request is approved, the feed will automatically be added to the database.

_Option 2:_ Edit the [data/feeds.csv](data/feeds.csv) file using a text editor and then send us a [pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests).

### How to edit feed description?

_Option 1:_ Send a request through this [form](https://github.com/iptv-org/database/issues/new?assignees=&labels=feeds%3Aedit&projects=&template=5_feeds_edit.yml&title=Edit%3A+). Specify the ID of the channel and feed you want to edit and the new data. To delete a value, insert `~` in the desired field. After your request is approved, the feed description will be automatically updated.

_Option 2:_ Edit the [data/feeds.csv](data/feeds.csv) file using a text editor and then send us a [pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests).

### How to remove a feed from the database?

Just fill out this [form](https://github.com/iptv-org/database/issues/new?assignees=&labels=feeds%3Aremove&projects=&template=6_feeds_remove.yml&title=Remove%3A+).

## Data Scheme

### channels

| Field          | Description                                                                                                                                                                                                                                                                                 | Required | Example                        |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ------------------------------ |
| id             | Unique channel ID derived from the `name` and `country` separated by dot. May only contain Latin letters, numbers and dot.                                                                                                                                                                  | Required | `AnhuiTV.cn`                   |
| name           | Official channel name in English or call sign. May include: `a-z`, `0-9`, `space`, `-`, `!`, `:`, `&`, `.`, `+`, `'`, `/`, `»`, `#`, `%`, `°`, `$`, `@`, `?`, <code>\|</code>, `¡`.                                                                                                         | Required | `Anhui TV`                     |
| alt_names      | List of alternative channel names separated by `;`. May contain any characters except `,` and `"`.                                                                                                                                                                                          | Optional | `安徽卫视;AHTV`                |
| network        | Network of which this channel is a part. May contain any characters except `,` and `"`.                                                                                                                                                                                                     | Optional | `Anhui`                        |
| owners         | List of channel owners separated by `;`. May contain any characters except `,` and `"`.                                                                                                                                                                                                     | Optional | `China Central Television`     |
| country        | Country code from which the channel is transmitted. A list of all supported countries and their codes can be found in [data/countries.csv](data/countries.csv)                                                                                                                              | Required | `CN`                           |
| subdivision    | Code of the subdivision (e.g., provinces or states) from which the broadcast is transmitted. A list of all supported subdivisions and their codes can be found in [data/subdivisions.csv](data/subdivisions.csv).                                                                           | Optional | `CN-AH`                        |
| city           | The name of the city in English from which the channel is broadcast. May contain any characters except `,` and `"`.                                                                                                                                                                         | Optional | `Hefei`                        |
| broadcast_area | [DEPRECATED] List of codes describing the broadcasting area of the channel separated by `;`. Any combination of `r/<region_code>`, `c/<country_code>`, `s/<subdivision_code>`.                                                                                                              | Required | `c/CN;r/ASIA`                  |
| languages      | [DEPRECATED] List of languages in which the channel is broadcast separated by `;`. A list of all supported languages and their codes can be found in [data/languages.csv](data/languages.csv).                                                                                              | Required | `zho;eng`                      |
| categories     | List of categories to which this channel belongs separated by `;`. A list of all supported categories can be found in [data/categories.csv](data/categories.csv).                                                                                                                           | Optional | `animation;kids`               |
| is_nsfw        | Indicates whether the channel broadcasts adult content (`TRUE` or `FALSE`).                                                                                                                                                                                                                 | Required | `FALSE`                        |
| launched       | Launch date of the channel (`YYYY-MM-DD`).                                                                                                                                                                                                                                                  | Optional | `2016-07-28`                   |
| closed         | Date on which the channel closed (`YYYY-MM-DD`).                                                                                                                                                                                                                                            | Optional | `2020-05-31`                   |
| replaced_by    | The ID of the channel that this channel was replaced by.                                                                                                                                                                                                                                    | Optional | `CCTV1.cn`                     |
| website        | Official website URL.                                                                                                                                                                                                                                                                       | Optional | `http://www.ahtv.cn/`          |
| logo           | Logo URL. Only URL with [HTTPS](https://ru.wikipedia.org/wiki/HTTPS) protocol are allowed. Supported image types: `PNG`, `JPEG`. Max size: 512x512 pixels. The link should not be [geo-blocked](https://en.wikipedia.org/wiki/Geo-blocking). May contain any characters except `,` and `"`. | Required | `https://example.com/logo.png` |

### feeds

| Field          | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Required | Example               |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | --------------------- |
| channel        | ID of the channel to which this feed belongs.                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Required | `HBO.us`              |
| id             | Unique feed ID derived from the `name`. May only contain Latin letters and numbers.                                                                                                                                                                                                                                                                                                                                                                                                                            | Required | `West`                |
| name           | Name of the feed in English. May include: `a-z`, `0-9`, `space`, `-`, `!`, `:`, `&`, `.`, `+`, `'`, `/`, `»`, `#`, `%`, `°`, `$`, `@`, `?`, <code>\|</code>, `¡`.                                                                                                                                                                                                                                                                                                                                              | Required | `West`                |
| is_main        | Indicates if this feed is the main for the channel (`TRUE` or `FALSE`).                                                                                                                                                                                                                                                                                                                                                                                                                                        | Required | `FALSE`               |
| broadcast_area | List of codes describing the broadcasting area of the feed separated by `;`. Any combination of `r/<region_code>`, `c/<country_code>`, `s/<subdivision_code>` is allowed. A full list of supported codes can be found here: [data/countries.csv](https://github.com/iptv-org/database/blob/master/data/countries.csv), [data/subdivisions.csv](https://github.com/iptv-org/database/blob/master/data/subdivisions.csv), [data/regions.csv](https://github.com/iptv-org/database/blob/master/data/regions.csv). | Required | `s/US-CA;s/US-ID`     |
| timezones      | List of timezones in which the feed is broadcast separated by `;`. A list of all supported timezones and their codes can be found in [data/timezones.csv](data/timezones.csv).                                                                                                                                                                                                                                                                                                                                 | Required | `America/Los_Angeles` |
| languages      | List of languages in which the feed is broadcast separated by `;`. A list of all supported languages and their codes can be found in [data/languages.csv](data/languages.csv).                                                                                                                                                                                                                                                                                                                                 | Required | `eng;spa`             |
| video_format   | Video format of the feed.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Required | `1080i`               |

### categories

| Field | Description   | Required | Example |
| ----- | ------------- | -------- | ------- |
| id    | Category ID   | Required | `news`  |
| name  | Category name | Required | `News`  |

### languages

| Field | Description                                                               | Required | Example    |
| ----- | ------------------------------------------------------------------------- | -------- | ---------- |
| name  | Official language name                                                    | Required | `Croatian` |
| code  | [ISO 639-3](https://en.wikipedia.org/wiki/ISO_639-3) code of the language | Required | `hrv`      |

### countries

| Field     | Description                                                                                                                                             | Required | Example   |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | --------- |
| name      | Official name of the country                                                                                                                            | Required | `Canada`  |
| code      | [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) code of the country                                                              | Required | `CA`      |
| languages | List of official languages of the country separated by `;`. A list of all supported languages can be found in [data/languages.csv](data/languages.csv). | Required | `eng;fra` |
| flag      | Country flag emoji                                                                                                                                      | Required | `🇨🇦`      |

### subdivisions

| Field   | Description                                                                                | Required | Example            |
| ------- | ------------------------------------------------------------------------------------------ | -------- | ------------------ |
| country | [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) code of the country | Required | `CA`               |
| name    | Official subdivision name                                                                  | Required | `British Columbia` |
| code    | [ISO 3166-2](https://en.wikipedia.org/wiki/ISO_3166-2) code of the subdivision             | Required | `CA-BC`            |

### regions

| Field     | Description                                                                                                            | Required | Example          |
| --------- | ---------------------------------------------------------------------------------------------------------------------- | -------- | ---------------- |
| name      | Official name of the region                                                                                            | Required | `Central Asia`   |
| code      | Abbreviated designation for the region. May only contain Latin letters in upper case. The minimum length is 3 letters. | Required | `CAS`            |
| countries | List of country codes in the region                                                                                    | Required | `KG;KZ;TJ;TM;UZ` |

### timezones

| Field      | Description                                                               | Required | Example               |
| ---------- | ------------------------------------------------------------------------- | -------- | --------------------- |
| id         | Timezone ID from [tz database](https://en.wikipedia.org/wiki/Tz_database) | Required | `Africa/Johannesburg` |
| utc_offset | [UTC offset](https://en.wikipedia.org/wiki/UTC_offset) for this time zone | Required | `+02:00`              |
| countries  | List of countries included in this time zone                              | Required | `ZA;LS;SZ`            |

### blocklist

List of channels blocked at the request of copyright holders.

| Field   | Description                                     | Required | Example                           |
| ------- | ----------------------------------------------- | -------- | --------------------------------- |
| channel | Channel ID                                      | Required | `AnimalPlanetAfrica.us`           |
| reason  | Reason for blocking                             | Required | `dmca`                            |
| ref     | Link to removal request or DMCA takedown notice | Required | `https://example.com/issues/0000` |

## Channel Logo Guidelines

Since finding a suitable logo for the channel is not always possible, this list contains only recommendations and should just help you in choosing a logo from several options.

1. If the channel logo has several versions, it is better to choose a color one.

   That way there is less chance of the logo blending in with the background.

   <img src="https://user-images.githubusercontent.com/7253922/235551685-34cbb982-078f-42b8-9fb3-2800afc80abe.png" width="600"/>

2. If the logo has changed over time, use the latest version.

   <img src="https://user-images.githubusercontent.com/7253922/235551700-e2ee6823-c6bc-4688-ad4c-081911703f42.png" width="600"/>

3. If the channel has several versions of the logo, it is better to use the one used on air.

   <img src="https://user-images.githubusercontent.com/7253922/235551795-4d89c2bc-f9eb-4ac2-88d4-2149a870776f.png" width="600"/>

   <img src="https://user-images.githubusercontent.com/7253922/235551738-3e6680ff-af77-4d22-af6d-cbaab7400b66.png" width="600"/>

4. If there is a transparent background around the logo is better to cut it.

   That way it's much easier to scale the logo later.

   <img src="https://user-images.githubusercontent.com/7253922/235551815-b9925ac5-85ac-458a-bf0b-a9d57eb2547d.png" width="600"/>

## Project Structure

```
database/
├── .github/
|   ├── ISSUE_TEMPLATE      # issue templates for the repository
|   ├── workflows           # contains GitHub actions workflows
|   ├── CODE_OF_CONDUCT.md  # rules you shouldn't break if you don't want to get banned
├── .husky/
|   ├── pre-commit          # commands to run before each commit
├── .readme/
|   ├── preview.png         # image displayed in the README.md
├── data/                   # contains all data
├── scripts/                # contains all scripts used in the repository
├── tests/                  # contains tests to check the scripts
├── .prettierrc.js          # configuration file for Prettier
├── eslint.config.mjs       # configuration file for ESLint
├── package.json            # project manifest file
├── tsconfig.json           # configuration file for TypeScript
├── LICENSE                 # license text
├── CONTRIBUTING.md         # file you are currently reading
├── README.md               # project description displayed on the home page
```

## Scripts

These scripts are created to automate routine processes in the repository and make it a bit easier to maintain.

For scripts to work, you must have [Node.js](https://nodejs.org/en) installed on your computer.

To run scripts use the `npm run <script-name>` command.

- `act:check`: allows to run the [check](https://github.com/iptv-org/iptv/blob/master/.github/workflows/check.yml) workflow locally. Depends on [nektos/act](https://github.com/nektos/act).
- `act:update`: allows to run the [update](https://github.com/iptv-org/iptv/blob/master/.github/workflows/update.yml) workflow locally. Depends on [nektos/act](https://github.com/nektos/act).
- `act:deploy`: allows to run the [deploy](https://github.com/iptv-org/iptv/blob/master/.github/workflows/deploy.yml) workflow locally. Depends on [nektos/act](https://github.com/nektos/act).
- `db:validate`: checks the integrity of data.
- `db:export`: saves all data in JSON format to the `/.api` folder.
- `db:update`: triggers a data update using approved requests from issues.
- `lint`: сhecks the scripts for syntax errors.
- `test`: runs a test of all the scripts described above.

## Workflows

To automate the run of the scripts described above, we use the [GitHub Actions workflows](https://docs.github.com/en/actions/using-workflows).

Each workflow includes its own set of scripts that can be run either manually or in response to an event.

- `check`: runs the `db:validate` script when a new pull request appears, and blocks the merge if it detects an error in it.
- `update`: sequentially runs `db:update` and `db:validate` scripts and commits all the changes if successful.
- `deploy`: after each update of the [master](https://github.com/iptv-org/database/branches) branch runs the script `db:export` and then publishes the resulting files to the [iptv-org/api](https://github.com/iptv-org/api) repository.
