(case
                 when f.ssfd_seq_sub_cnt_list_plan is not null then
                  (select count(0)
                     from sceir sce1
                    where sce1.scea_cnt_list_id = f.ssfd_seq_sub_cnt_list_plan
                      and sce1.scea_cancel_flag = 'N'
                      and sce1.scea_release_time >=
                          to_date('2021-04-01 00:00:00', 'yyyy-mm-dd hh24:mi:ss'))
                 when f.ssfd_eir_id is not null then
                  (select count(0)
                     from sceir sce1
                    where sce1.scea_eir_id = f.ssfd_eir_id
                      and sce1.scea_cancel_flag = 'N'
                      and sce1.scea_release_time >=
                          to_date('2021-04-01 00:00:00', 'yyyy-mm-dd hh24:mi:ss'))
                 else
                  (select count(0)
                     from sceir sce1
                    where sce1.scea_eir_no = f.ssfd_eir_no
                      and sce1.scea_cancel_flag = 'N'
                      and sce1.scea_release_time >=
                          to_date('2021-04-01 00:00:00', 'yyyy-mm-dd hh24:mi:ss'))
               end) > 0
           and (case
                 when f.ssfd_seq_sub_cnt_list_plan is not null then
                  (select count(0)
                     from sceir sce1
                    where sce1.scea_cnt_list_id = f.ssfd_seq_sub_cnt_list_plan
                      and sce1.scea_cancel_flag = 'N'
                      and sce1.scea_release_time <
                          to_date('2021-04-30 00:00:00', 'yyyy-mm-dd hh24:mi:ss') + 1)
                 when f.ssfd_eir_id is not null then
                  (select count(0)
                     from sceir sce1
                    where sce1.scea_eir_id = f.ssfd_eir_id
                      and sce1.scea_cancel_flag = 'N'
                      and sce1.scea_release_time <
                          to_date('2021-04-30 00:00:00', 'yyyy-mm-dd hh24:mi:ss') + 1)
                 else
                  (select count(0)
                     from sceir sce1
                    where sce1.scea_eir_no = f.ssfd_eir_no
                      and sce1.scea_cancel_flag = 'N'
                      and sce1.scea_release_time <
                          to_date('2021-04-30 00:00:00', 'yyyy-mm-dd hh24:mi:ss') + 1)
               end) > 0
           and f.ssfd_org_id = ssiv.ssiv_org_id(+)
           and f.ssfd_org_id = sb.ssbi_org_id(+))