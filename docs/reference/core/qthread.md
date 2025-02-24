<!--
SPDX-FileCopyrightText: 2022 Daniel Vrátil <dvratil@kde.org>

SPDX-License-Identifier: GFDL-1.3-or-later
-->

# QThread

{{ doctable("Core", "QCoroThread") }}

[`QThread`][qtdoc-qthread] has two events: `started` and `finished`. QCoro provides
a coroutine-friendly wrapper for `QThread` - `QCoroThread`, which allows `co_await`ing
those events.

To wrap a `QThread` object into the `QCoroThread` wrapper, use [`qCoro()`][qcoro-coro]:

```cpp
QCoroThread qCoro(QThread &);
QCoroThread qCoro(QThread *);
```

## `waitForStarted()`

Waits for the thread to start. Returns `true` if the thread is already running
or when the thread starts within the specified timeout. If the thread has already
finished or fails to start within the specified timeout, the coroutine will return
`false`.

If the timeout is set to -1, the operation will never time out.

See documentation for [`QThread::started()`][qtdoc-qthread-started] for details.

```cpp
QCoro::Task<bool> QCoroThread::waitForStarted(std::chrono::milliseconds timeout);
```

## `waitForFinished()`

Waits for the Waits for the process to finish or until it times out. Returns `bool` indicating
whether the process has finished successfuly (`true`) or timed out (`false`).
thread to finish. Returns `true` if the thread has already finished
or if it finishes within the specified timeout. If the thread has not started yet
or fails to stop within the specified timeout the coroutine will return `false`.

If the timeout is set to -1, the operation will never time out.

See documentation for [`QThread::finished()`][qtdoc-qthread-finished] for details.

```cpp
QCoro::Task<bool> QCoroThread::waitForFinished(std::chrono::milliseconds timeout);
```

## Examples

```cpp
{% include "../../examples/qthread.cpp" %}
```


[qtdoc-qthread]: https://doc.qt.io/qt-5/qthread.html
[qtdoc-qthread-waitForStarted]: https://doc.qt.io/qt-5/qthread.html#waitForStarted
[qtdoc-qthread-waitForFiished]: https://doc.qt.io/qt-5/qthread.html#waitForFinished
[qcoro-coro]: ../coro/coro.md
