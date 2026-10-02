# Run Workflows in Forge Desktop

Forge Desktop can start an enabled workflow for an issue from the project launcher.

1. Open a project and enter an issue URL, a tracker key such as `ENG-123`, or a numeric issue ID.
2. Choose a workflow, or leave the selector on **Auto** and select **Suggest workflow** to have
   Forge recommend one after reading the issue (when routing is enabled in `project.toml`).
3. Select **Run workflow**. Forge starts the workflow through the project engine for that issue.
   The issue applies to this run only; the project's saved issue context (set by
   `frg config set-issue`) is left unchanged.
4. Follow the run on its task page. The page receives replayed and live engine events, shows stage
   progress, and prompts for approval or input when the workflow requires it. Use **Cancel** to
   request cancellation from the engine. After cancellation, choose **Run again** to start from the
   beginning, or **Start from…** to select a step the workflow author recommends as a start point.
   Both actions create a fresh run; starting from a later step skips earlier steps and does not
   resume the cancelled run or undo side effects from the previous run. Before starting there,
   verify that the selected step's prerequisites are already satisfied. Forge Desktop offers only
   steps marked `is_entry_point = true` in the workflow definition; the CLI accepts any state.

The launcher validates the reference format locally; it does not check whether the issue exists in
the external tracker. The engine remains authoritative for workflow, project, and execution
validation.

Runs are hosted by the desktop app's project engine. Event replay provides the history retained by
the engine, but does not make execution continue after the host process exits.

Workflow file artifacts appear inside the step that produced them. Choose **Read** to preview a
UTF-8 text file in Forge Desktop (up to 1 MiB), or **Show in Finder** (**Show in File Explorer**
on Windows) to locate the file in the system's file manager. Forge Desktop never launches artifact
files directly. Binary, oversized, or out-of-job files cannot be previewed.

In **Advanced options** of the launcher, **Start from** lists only the workflow's initial state and
states marked `is_entry_point = true`, and **Ends at** lists only later states marked
`is_exit_point = true`.

A project runs one workflow at a time. A workflow blocks new workflows only while the project
engine is still running it; once it completes, fails, is cancelled, or is interrupted, you can start
another workflow or choose **Run again**.

## Run a Single Command

Select **Command** in the launcher to run one Forge command (for example `issue draft` or `ask`)
instead of a whole workflow.

1. Choose a command. Forge Desktop lists only the commands and options the project engine accepts.
2. Enter the issue, pull request, or support ticket the command needs, and any options or
   instructions.
3. Select **Run command**. Forge starts the command through the project engine, the same way the
   CLI does.

Unlike a workflow's issue, an issue, pull request, or ticket ID supplied to a command is saved as
the project's context, exactly like `frg config set-issue`, `frg config set-pr`, or
`frg config set-ticket`. Later CLI commands in the project use it too. A command without IDs uses
the project's saved context. The IDs are saved only once the engine accepts the command.

While a run is in progress, Forge Desktop refuses to switch the project to a different issue,
pull request, or ticket than the run's or the saved one, including a pull request the run created:
wait for that run to finish, or run the command for the same item. CLI commands such as
`frg config set-issue` write the saved context directly and are not checked.

Follow the command on its task page, which shows its progress. Use **Cancel** to request
cancellation from the engine. If the command cannot start (for example, you are signed out, a
required ID is missing, or another run is using the project's context), the launcher shows the
reason; if it fails while running, its task page shows the engine's error.