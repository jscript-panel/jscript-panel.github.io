- Always check the method arguments for the type/range of values you can supply. Over the years, internal validation has got stricter and errors may be thrown when they were silently ignored before.
- If anything goes wrong, check the popup window/console. It should tell you where the code is that caused the error.
- Never call `window.Repaint()` or `window.RepaintRect()` from the `on_size` callback.
- Consider using `Dispose()` methods where you can to free up memory.
- Remember to retrieve `window.Width` and `window.Height` in the `on_size` callback because their values during startup is not reliable.
- You should not create objects inside the `on_paint` callback since it will be called frequently. For example, `utils.LoadImage` and `fb.TitleFormat` should never be used there. Ideally, these objects should be created once on startup.
