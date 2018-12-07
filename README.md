# Extra
Extra
tabela = read_csv('alunos.csv')
ggplot(tabela,aes(x=tempo))+
  geom_histogram(aes(y=..density..),bins =  20)+
  stat_function(aes(x=tempo),fun=dexp,args = list(rate=1/50))

ggplot(tabela,aes(sample=tempo))+
  stat_qq(distribution = stats::qexp)+
  stat_qq_line(distribution = stats::qexp)

#teste de aderencia
a=quantile(tabela$tempo,0.25);a
b=quantile(tabela$tempo,0.50);b
c=quantile(tabela$tempo,0.75);c
tabela$gp = cut(tabela$tempo,
      breaks=c(-Inf,18.5,39.5,80.75 ,Inf),
      labels=c('<a','>a e <b','>b e <c','>c'))
p1=pexp(18.5,rate = 1/50);p1
p2=pexp(39.5,rate = 1/50)-p1;p2
p3=pexp(80.75,rate = 1/50)-p1-p2;p3
p4=pexp(80.75,rate = 1/50,lower.tail = F);p4
chisq.test(tabela$gp)
