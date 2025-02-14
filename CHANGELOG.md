# Changelog

## 0.2.10 (August 12, 2019)

- Fixed typings for `stateTableForScopes` and `stateTableForAccounts` that was not correct
  according to dfuse REST API.

## 0.2.9 (August 12, 2019)

- Fixed typings for `StateTableScopesResponse` that was not correct
  according to dfuse REST API.

## 0.2.8 (July 26, 2019)

- Bumped development dependencies.
- Typo in example file (thanks @marcuswin).

## 0.2.7 (July 26, 2019)

- Added support for `Worbli` network straight in the library.

## 0.2.6 (May 24, 2019)

- Improves WebSocket streaming reference examples to better
  show the message flow.

- Fixed basic streaming examples that were not behaving as
  expected due to a bug.

- Added a `release` method on all interfaces used by the
  `DfuseClient` so a release of some hold handles can be
  performed.

- Added `endpoints` getter on `DfuseClient` to reduce code
  required when using Apollo Link.

## 0.2.5 (May 2, 2019)

- Added a check to ensure the API key provided to `createDfuseClient`
  is actually a valid API key. A specialized message being displayed to
  those using an API token instead.

## 0.2.4 (April 30, 2019)

- Renamed `ActionTraceData` `DbOp` to `ActionTraceDbOp`. This fixes
  a problem where `DbOp` type from library was always the `TableDeltaData`
  one since they were conflicting having the same name. This rename is **not**
  a breaking change since it was impossible to import the type.

- Fix `ActionTraceData` `dbops` field definition which was incorrectly
  using `TableDeltaData` `DbOp` definition while not being the same at all.

  **Warning** Requires some modification steps (resolving new compilation
  errors for some usage of the library's types). See
  [From '@dfuse/client@0.2.3' to '@dfuse/client@0.2.4'](./MIGRATION.md#from-dfuseclient023-to-dfuseclient024)
  section in migration guide.

- Removed duplicated `DbOp` definition which was wrong anyway.

- Deprecated `RAMOP` (renamed to `RamOp`).

- Deprecated `DBOp` (renamed to `DbOp`).

## 0.2.3 (April 30, 2019)

- Fixed typing mismatch between dfuse WebSocket API JSON output
  and our own type definitions.

  **Warning** Requires some modification steps (resolving new compilation
  errors for some usage of the library's types). See
  [From '@dfuse/client@0.2.2' to '@dfuse/client@0.2.3'](./MIGRATION.md#from-dfuseclient022-to-dfuseclient023)
  section in migration guide.

## 0.2.2 (April 26, 2019)

- Added support for `GET /v0/block_id/by_time` endpoint.

- Added possibility to get a valid API token straight from the dfuse Client
  instance. This enables consumer of our GraphQL API to delegate API key
  management logic to `@dfuse/client` library.

## 0.2.1 (April 24, 2019)

- Fixed dfuse Search API `blockCount` default value that was larger
  than a Uint32 value being the biggest value accepted by dfuse API.

- Added support for `GET /v0/transactions/:id` endpoint.

- Added `matchingActionTraces` helper to easily extract a
  the matching action traces out of a `SearchTransactionRow` when performing
  a search query through dfuse REST API search endpoint.

- Added `flattenActionTraces` helper to easily extract action traces
  from a `TransactionLifecycle` object (useful to find matching action
  for action index used by dfuse API).

- Fixed a bunch of typing errors between actual `nodeos` JSON output
  and our own type definitions as well against dfuse API directly.
  **Warning** Requires some modification steps (resolving new compilation
  errors for some usage of the library's types). See [From '@dfuse/client@0.2.0' to '@dfuse/client@0.2.1'](./MIGRATION.md#from-dfuseclient020-to-dfuseclient021) section in migration guide.

## 0.2.0 (April 23, 2019)

- Removed `socket` public property from `StreamClient` interface to
  reduce coupling.

- It's now possible to add custom headers when using
  `DfuseClient.apiRequest` method (same on underlying `HttpClient`
  interface).

- Now exposing `dfuseClient.apiRequest` as a public method of the
  `DfuseClient` interface.

- Fixed UMD build that was not minified anymore due to an oversight.

- Fixed UMD build that incorrectly had `require(...)` clauses and
  that could be picked for transformation by some bundler tool.

- The function `isExpiredOrNearExpiration` has been renamed to
  `isApiTokenExpired` to better reflect the intention of the method.

- Changed default reconnect delay value from `5s` to `2.5s`.

- Added a `Stream.onPostRestart` callback that can be used to act after a
  successful stream restart, see [./examples/advanced/never-miss-a-beat.ts]
  for usage.

- Fixed a bug where re-connect was not connected back if an error
  occurred in the reconnect itself.

- Added a `OnDiskApiTokenStore` to store the token under
  `~/.dfuse/<sha256-api-key>/token.json` file using the `FileApiTokenStore`
  and make it the default in a Node.js environment.

- Added a `FileApiTokenStore` to store the token info under a given file
  (can be used only in a Node.js environment).

- Added `LocalStorageApiTokenStore` implementation and make it the default
  in a Browser environment.

- Now distributing an `es5` and `umd` build in addition to the old previous
  `commonjs` build (now under `dist/lib`).

- Added `dynamicMessageDispatcher` helper to easily create an `OnStreamMessage`
  that dispatches to correct handler based on the message's type.

- Streams now auto-restart at last marked block if present or at provided
  value upon socket re-connection.

- Add full support for marking the stream at the right location.

- Renamed the library to `@dfuse/client`.

- Major overhaul of the full API of the library to become a full dfuse Client library,
  read the `MIGRATION.md` guide for more details on how to go from `@dfuse/eosws-js` to
  the full blown `@dfuse/client`.

### From 0.2.0-rc.2 to 0.2.0-rc.3

- The `unlisten` function of a `Stream` (has returned by `registerStream`), has
  been renamed to `close`. Simply rename the method to upgrade.

## In Progress (Current)

## 0.11.11 (March 26, 2019)

- Fixed a bug where `onClose` event was not notified anymore when if error occurred before closing WebSocket.

## 0.11.10 (March 26, 2019)

- Fixed a bug where `onClose` event was not notified on closing of the WebSocket connection.

## 0.11.9 (March 25, 2019)

- Added an option to specify the amount of time in milliseconds between each keep alive messages.

## 0.11.8 (March 22, 2019)

- Passing socket event to `onError` and `onClose` event handlers.
- Added `trace_id` to error type.

## 0.11.7 (March 21, 2019)

- Added possibility to pass undocumented options.

## 0.11.6 (December 02, 2018)

- Fixed `with_progress` accepting a `number` and not a `boolean`.

## 0.11.5 (November 28, 2018)

- Updated multi contracts example to use the new `accounts` parameter.
- Updated library to support new version of `get_action_traces` (added `accounts`, `receivers` and `action_names`).

### Deprecations

Those are deprecation notices, they are still available in the current pre-release major version
(`0.11.x` in this case). You are welcome to upgrade right now however.

- Renamed `GetActionTracesMessageData#account` to `GetActionTracesMessageData#accounts`.
- Renamed `GetActionTracesMessageData#receiver` to `GetActionTracesMessageData#receivers`.
- Renamed `GetActionTracesMessageData#action_name` to `GetActionTracesMessageData#action_names`.

## 0.11.4 (November 22, 2018)

- Fix back to back connect()

## 0.11.3 (November 16, 2018)

- Reverted `Fix client connection flow`, this was preventing examples from running correctly.

## 0.11.2 (November 16, 2018)

- Fixed version
- Fix DBOp interface
- Fix client connection flow
- Update examples

## 0.11.1 (November 9, 2018)

- Fixed README to read `getTransactionLifecycle` in the API section.

## 0.11.0 (November 9, 2018)

### Breaking Changes

- Renamed `EoswsClient.getTransaction` to `EoswsClient.getTransactionLifecycle`.
- Renamed `getTransactionMessage` to `getTransactionLifecycleMessage`.
- Renamed `OutboundMessageType.TRANSACTION` to `OutboundMessageType.TRANSACTION_LIFECYCLE`.

## 0.10.0 (November 9, 2018)

### Breaking Changes

- Removed all previous code, everything has been replaced by a proper `EoswsClient` object.

#### Package

The previous package was mostly released on name `eosws`. The package has been migrated to
our `dfuse` branding instead, so first, you will need to update that.

    yarn remove eosws
    yarn add @dfuse/eosws-js

or using NPM:

    npm uninstall --save @dfuse/eosws-js
    npm install --save @dfuse/eosws-js

#### Listening

Instead of:

    import { get_actions, parse_actions } from 'eoswjs'

    const endpoint = 'mainnet.eos.dfuse.io'
    const origin = 'https://example.com'
    const token = '<Paste your API token here>'

    const ws = new WebSocket(`wss://${endpoint}/v1/stream?token=${token}`, { origin })

    ws.onopen = () => {
      ws.send(get_actions({ accounts: 'eosio.token', action_names: 'transfer' }))
    }

    ws.onmessage = (message) => {
      const actions = parse_actions(message.data)

      if (actions) {
        const { from, to, quantity, memo } = actions.data.trace.act.data
        console.log(from, to, quantity, memo)
      }
    }

You should replace with:

    import { EoswsClient, createEoswsSocket, InboundMessageType } from '@dfuse/eosws-js'

    const endpoint = 'mainnet.eos.dfuse.io'
    const token = '<Paste your API token here>'
    const client = new EoswsClient(createEoswsSocket(() =>
        new WebSocket(`wss://${endpoint}/v1/stream?token=${token}`, { origin: 'https://example.com' })))

    client.connect().then(() => {
        client
            .getActionTraces({ accounts: 'eosio.token', action_names: 'transfer' })
            .onMessage((message) => {
                if (message.type === InboundMessageType.ACTION_TRACE) {
                    const { from, to, quantity, memo } = message.data.trace.act.data
                    console.log(from, to, quantity, memo)
                }
            })
    })

#### Parsing Messages

This functionality has been removed completely, you will need to make the checking by "hand":

    onMessage = (message) => {
        if (message.type === 'action_trace') {
            console.log('Action trace, do something useful.')
        }
    }

#### Creating Messages

If you only want to create messages, the functionality is still available. Instead of doing:

    import { get_actions } from 'eoswjs'

    // ... WebSocket stuff here

    ws.send(get_actions({ accounts: 'eosio.token', action_names: 'transfer' }))

Do this instead:

    import { getActionTracesMessage } from '@dfuse/eosws-js'

    ws.send(getActionTracesMessage({ accounts: 'eosio.token', action_names: 'transfer' }))

Here the list of available message constructors:

- `getActionTracesMessage`
- `getTableRowsMessage`
- `getTransactionLifecycleMessage`

**Note** Those constructors are not documented yet as part of the API and might be removed
in the future, this has not been decided yet. Refer to the [src/message/outbound.ts](./src/message/outbound.ts)
file for available parameters for each constructors.

### Improvements

- Added a proper `EoswsSocket` that automatically re-connects on abnormal closing.
- Added a proper `EoswsClient` to wrap all operations correctly.
- Overhaul of examples and supporting documentation.

## 0.9.2 (October 31, 2018)

- On `get_actions` & `get_table_deltas` only has two params (data parameters & optional parameters) both as defined as Objects.
- On `get_actions`, `receiver` is now optional and defaults to the same value as `account`.
- The `get_table_deltas` request was renamed to `get_table_rows`.
