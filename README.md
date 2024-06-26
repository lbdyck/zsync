# zsync
ISPF application to sync two partitioned dataset

zSync is an ISPF Dialog that will compare two, non-load library,
partitioned data sets. The user will be presented with a ISPF table with
all listed members along with the state of each member. The state will
indicate if the member is eligible to be copied.

With the ISPF Dialog there is an option to enter the volsers for the
from and to datatsets. This is not available using the command.

All default comparisons to determine copy eligibility are done using
ISPF Services.  If either, or both, members have no ISPF stats then the
members are compared using the ISPF Edit compare and the state and copy
eligible flag are then set accordingly.

Note: Truncation can occur if the source PDS has a larger LRECL than
      the target PDS. When this is detected the dialog informs the user
      via messages on the member display panel with the RECFM and LRECL
      of the From and To libraries and a warning message.

The available Commands are:

   Copy       Copy all eligible members
              Copy information is placed in the ISPF Log
   Locate     Locate the member in the list, a partial name is accepted
              L abc
   Only       Display only the copy eligible members
   Refresh    Refresh the member list display
              Ref or Ref member-pattern
   Save       Generate a report of all the members in the display
              with ispf stats and a delta indicator
   Sort       Sort the list in member or state order
              S Mem A/D or S State A/D
              A = ascending (default) D = descending
   ZSWAP      Refresh and swap the from and to datasets

The available line selection options are:

    B       - Browse the From member
    BT      - Browse the To member
    C       - ISPF Edit Compare
    CD      - Check for Delta using SuperC
    CS      - Check for Delta using SuperC Compare and View results
    E       - Edit the From member
    ET      - Edit the To member
    I       - ISPF Stats
    S or /  - Display Selection prompt
    X       - Exclude the member
    Z       - Copy selected member

The syntax is:

   %zSync from-pds to-pds member-pattern \ option

The from and to partitioned data set names are optional and if not
provided the user will be prompted for them.

 The option must follow the \ and may be:

        valid options:

        all             ignore ispf stats and do a compare on all
                        members
        once            process and then exit
        only            allowed with either other option and only
                        display delt members
