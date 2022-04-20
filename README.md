# encuesta

def best_dude(alias, df): 
    dudes={}   

    xedad=int(df[df['alias']==alias]['rango_edad_level'])
    xintro=int(df[df['alias']==alias]['p_introvertido_level'])
    xextro=int(df[df['alias']==alias]['p_extrovertido_level'])
    xmascota=int(df[df['alias']==alias]['mascota_level'])   

    # Principales ------
    yedad=0
    diff_edad=0
    diff_intro=0
    diff_extro=0
    diff_mascota=0
    #-----------------   
    total=0

    for index, row in df.iterrows():
        if row['alias']!=alias:        
            diff_edad=abs(xedad-int(row['rango_edad_level']))
            diff_intro=abs(xintro-int(row['p_introvertido_level']))
            diff_extro=abs(xextro-int(row['p_extrovertido_level']))
            diff_mascota=abs(xmascota-int(row['mascota_level']))            
            total=diff_edad+diff_intro+diff_extro+diff_mascota  
            dudes[row['alias']]=total

    df_dudes = pd.DataFrame(list(dudes.items()),columns = ['alias','cerca']) 
    df_dudes=df_dudes[df_dudes['cerca']<=2].sort_values(by="cerca")

    return df_dudes
