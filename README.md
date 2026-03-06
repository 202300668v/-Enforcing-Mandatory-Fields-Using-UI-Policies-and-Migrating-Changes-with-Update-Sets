# -Enforcing-Mandatory-Fields-Using-UI-Policies-and-Migrating-Changes-with-Update-Sets
(function executeRule(current, previous /*null when async*/) {

    var incGr = new GlideRecord('incident');
    incGr.addQuery('assigned_to', current.sys_id);
    incGr.setLimit(1); // Just need to check existence

    // incGr.addQuery('active', true); we can use the above or this line of code to
    // check where the user is assigned with any incident

    incGr.query();

    if (incGr.next()) {
        gs.addErrorMessage('This user cannot be deleted because they are assigned to one or more incidents.');
        current.setAbortAction(true);
    }

    // Add your code here

})(current, previous);
