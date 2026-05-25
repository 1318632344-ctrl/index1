
import React, { useState, useEffect, useRef } from 'react';
import { 
  Tv, 
  History, 
  Play, 
  ChevronLeft, 
  ChevronRight, 
  Video, 
  MessageSquare, 
  Info,
  X,
  FileText,
  User,
  ThumbsUp,
  AlertCircle,
  Clock,
  Sparkles,
  HelpCircle,
  RotateCcw,
  Compass,
  CheckCircle2,
  Lightbulb,
  Navigation,
  Mic
} from 'lucide-react';

const CLIENT_CARD = {
  title: '专业型客户',
  description:
    '直接询问其某一个功能，功能后的价值，某一个功能点的细节，向销售发起反问，让其给与承诺，对比竞品，问题较难。',
};

const DRILL_STEPS_NO_PPT = [
  { title: '环节1: 环境破冰', desc: '开场白、建立初步联系、缓和气氛的对话' },
  { title: '环节2: 公司、产品核心价值传递', desc: '系统地介绍公司的背景、实力、资力和信誉' },
  { title: '环节3: 需求挖掘', desc: '通过提问了解客户痛点、需求、预算等' },
  { title: '环节4: 商务洽谈与关单环节', desc: '促成交易、确认合作意向的阶段' },
];

const DRILL_STEPS_WITH_PPT = [
  { title: '环节1: 环境破冰', desc: '开场白、建立初步联系、缓和气氛的对话' },
  { title: '环节2: 材料宣讲', desc: '选择并讲解带来的 PPT 资料，传递产品价值' },
  { title: '环节3: 公司、产品核心价值传递', desc: '系统地介绍公司的背景、实力、资力和信誉' },
  { title: '环节4: 需求挖掘', desc: '通过提问了解客户痛点、需求、预算等' },
  { title: '环节5: 商务洽谈与关单环节', desc: '促成交易、确认合作意向的阶段' },
];

const DEMO_SCENARIOS = [
  {
    id: 'first_no_ppt',
    cardNo: '01',
    actionLabel: '开启首次实战（无材料宣讲）',
  },
  {
    id: 'first_with_ppt',
    cardNo: '02',
    actionLabel: '开启首次实战（含材料宣讲）',
  },
  {
    id: 'continue_before_ppt',
    cardNo: '03',
    actionLabel: '继续回合实战（宣讲前继续）',
  },
  {
    id: 'continue_after_ppt',
    cardNo: '04',
    actionLabel: '继续回合实战（宣讲后继续）',
  },
];

const AnimeAvatar = () => (
  <svg viewBox="0 0 200 240" className="w-48 h-56 mx-auto drop-shadow-md">
    <circle cx="100" cy="110" r="85" fill="#F8FAFC" stroke="#E2E8F0" strokeWidth="1" />
    <path d="M55,90 C45,110 45,150 50,170 C55,160 55,120 60,100 Z" fill="#6B4423" />
    <path d="M145,90 C155,110 155,150 150,170 C145,160 145,120 140,100 Z" fill="#6B4423" />
    <path d="M50,80 C40,110 40,180 50,200 C52,200 55,170 58,150 Z" fill="#5C3A1E" />
    <path d="M150,80 C160,110 160,180 150,200 C148,200 145,170 142,150 Z" fill="#5C3A1E" />
    <rect x="92" y="145" width="16" height="25" rx="4" fill="#FCE5D8" />
    <path d="M92,160 L108,160 L100,170 Z" fill="#EAD0C3" />
    <path d="M60,95 C60,65 140,65 140,95 C140,135 130,155 100,155 C70,155 60,135 60,95 Z" fill="#FFEFE5" />
    <path d="M58,105 C54,105 54,115 58,118 Z" fill="#FFE5D9" />
    <path d="M142,105 C146,105 146,115 142,118 Z" fill="#FFE5D9" />
    <ellipse cx="82" cy="103" rx="8" ry="11" fill="#2E231D" />
    <ellipse cx="80" cy="100" rx="3" ry="4" fill="#FFFFFF" />
    <ellipse cx="84" cy="106" rx="1" ry="1.5" fill="#FFFFFF" opacity="0.7" />
    <path d="M72,94 C76,90 88,90 92,94" stroke="#2E231D" strokeWidth="2.5" strokeLinecap="round" fill="none" />
    <ellipse cx="118" cy="103" rx="8" ry="11" fill="#2E231D" />
    <ellipse cx="120" cy="100" rx="3" ry="4" fill="#FFFFFF" />
    <ellipse cx="116" cy="106" rx="1" ry="1.5" fill="#FFFFFF" opacity="0.7" />
    <path d="M108,94 C112,90 124,90 128,94" stroke="#2E231D" strokeWidth="2.5" strokeLinecap="round" fill="none" />
    <ellipse cx="74" cy="116" rx="6" ry="3" fill="#FF8A8A" opacity="0.4" />
    <ellipse cx="126" cy="116" rx="6" ry="3" fill="#FF8A8A" opacity="0.4" />
    <path d="M100,114 L99,119 L101,119 Z" fill="#E2C1B0" />
    <path d="M95,130 Q100,135 105,130" stroke="#7C5034" strokeWidth="1.5" strokeLinecap="round" fill="none" />
    <path d="M73,83 Q82,77 90,82" stroke="#4A311E" strokeWidth="2" strokeLinecap="round" fill="none" />
    <path d="M110,82 Q118,77 127,83" stroke="#4A311E" strokeWidth="2" strokeLinecap="round" fill="none" />
    <path d="M60,95 Q100,45 140,95 C140,95 135,78 128,82 C120,85 112,98 108,103 C104,95 101,92 98,90 C95,88 90,92 88,95 C82,102 75,98 70,86 C65,78 60,95 60,95 Z" fill="#6B4423" />
    <path d="M72,70 Q100,55 128,70" stroke="#8E5E38" strokeWidth="2" strokeLinecap="round" fill="none" opacity="0.4" />
    <path d="M70,170 L130,170 L140,240 L60,240 Z" fill="#F1C232" />
    <path d="M86,170 L114,170 L110,188 L90,188 Z" fill="#FFFFFF" />
    <path d="M86,170 L100,188 L90,188 Z" fill="#E2E8F0" />
    <path d="M114,170 L100,188 L110,188 Z" fill="#CBD5E1" />
    <path d="M96,188 L104,188 L106,204 L94,204 Z" fill="#C0392B" />
    <circle cx="100" cy="188" r="4" fill="#962D22" />
    <path d="M72,170 L90,188 L74,198 Z" fill="#D4A71C" />
    <path d="M128,170 L110,188 L126,198 Z" fill="#D4A71C" />
  </svg>
);

const PPT_LIST = [
  {
    id: "PPT-01",
    name: "制造业数字门户2026核心解决方案.pdf",
    uploadDate: "2026-05-18 10:00",
    isExamined: true,
    slidesCount: 3,
    coverColor: "from-blue-600 to-indigo-800",
    slides: [
      {
        page: 1,
        title: "第一页：传统制造企业的痛点与数字化诉求",
        content: "痛点分析：\n1. 信息孤岛：研发、生产、销售数据未打通，协同效率低下。\n2. 客户触达慢：依赖传统渠道，无法直接获取终端用户反馈。\n3. 交付周期长：供应链上下游不透明，生产排程难以灵活动态调整。",
        standardAnswer: "本页核心在于点出制造型企业面临的'数据孤岛'与'反馈滞后'。标准表达应强调：数字门户致力于打通销售与生产的最后一公里，通过集成API实现上下游数据实时流转，帮企业降本增效达20%以上。",
        userAnswer: "我们这个系统的主要功能是打破信息孤岛，把数据打通。然后，客户也可以在门户里面看到订单进度，生产排程也会变快，从而缩短交付周期。",
        score: 85,
        gapAnalysis: "表达了'打通数据'的基本意思，但缺乏量化数据支撑（如降本增效20%），且未能生动阐述'上下游实时集成'的具体操作方案。建议后续加强业务价值的定量描述。"
      },
      {
        page: 2,
        title: "第二页：数字门户的核心功能模块及矩阵",
        content: "功能矩阵：\n1. 客商在线：自助下单、合同流转、对账开票全线上完成。\n2. 智能客服：AI问答结合人工接待，7*24小时解决客户售后问题。\n3. 数据驾驶舱：大屏多维展示，实时把控业务走势与核心KPI指标。",
        standardAnswer: "本页演示重点应放在'业务闭环'上。要向客户展示从下单、履约、对账、售后的全流程无人化协同。重点提炼'智能客服'如何结合大模型，为客户提供1对1的管家式解答服务。",
        userAnswer: "第二页展示的是我们的功能。包括在线自助下单、合同和发票管理。还有24小时的AI客服解答问题。最后还有一个数据大屏，管理人员可以直接在后台看到KPI指标，非常方便。",
        score: 92,
        gapAnalysis: "结构十分清晰，功能点覆盖全面。在介绍'智能客服'时表现良好，但在阐述'客商在线'时，可进一步补充关于安全风控 and 合规合同流转的保障机制，使宣讲显得更为稳重可靠。"
      },
      {
        page: 3,
        title: "第三页：成功客户案例及量化核心价值",
        content: "标杆案例：\n- 某头部重工企业：部署数字门户后，客户自助下单率达95%以上，订单周期缩短35%。\n- 某汽车零部件厂商：客服满意度跃升至98%，对账效率提升3倍。\n- 价值总结：数字渠道聚合，构建专有流量阵阵，驱动业务高增长！",
        standardAnswer: "案例页说服力在于'真实场景'和'前后对比'。应讲清重工企业部署前后的具体困境。核心说辞：'以xx重工为例，以前他们下单靠人工对单易出错，接入我们门户后，95%自助下单，实现了零误差生产，周期缩短超三分之一。'",
        userAnswer: "第三页是成功案例。一个重工企业用我们的系统后，基本不用人工了，自助下单95%，订单快了35%。还有一个汽车厂商对账效率提高了3倍，用户反馈也更好了。所以我们系统很有价值。",
        score: 78,
        gapAnalysis: "案例说服力稍显平淡，'基本不用人工了'说法不够精准，容易引发客户对失业或系统鲁棒性的过度焦虑。建议改为：'实现了下单流程的自动化流转，解放人工进行高价值客户维护。'"
      }
    ]
  },
  {
    id: "PPT-02",
    name: "数字渠道提效与客商在线白皮书.pdf",
    uploadDate: "2026-05-20 14:30",
    isExamined: false,
    slidesCount: 2,
    coverColor: "from-teal-600 to-cyan-800",
    slides: [
      {
        page: 1,
        title: "第一页：客商在线的价值链重构",
        content: "将传统销售转为数字化客商协同，打通信息链路。",
        standardAnswer: "讲解重构的核心。",
        userAnswer: "略。",
        score: 0,
        gapAnalysis: "暂无数据"
      }
    ]
  },
  {
    id: "PPT-03",
    name: "制造业出海数字营销指南.pdf",
    uploadDate: "2026-05-21 09:15",
    isExamined: true,
    slidesCount: 1,
    coverColor: "from-purple-600 to-indigo-800",
    slides: [
      {
        page: 1,
        title: "第一页：出海营销痛点及打法",
        content: "海外流量获取成本高，转化率低，需要全链路营销闭环。",
        standardAnswer: "本页核心讲出海难题及数字营销全链路解决方案。",
        userAnswer: "出海营销成本高，我们需要好的打法。",
        score: 70,
        gapAnalysis: "略显单薄。"
      }
    ]
  }
];

function PptRoundCard({ round, selectedPPT, userPptAnswers, pptDetailPage, setPptDetailPage }) {
  if (!selectedPPT) return null;
  const slides = selectedPPT.slides;
  const sortedSlides = [...slides].sort((a, b) => a.score - b.score);
  const worstThree = sortedSlides.slice(0, 3);
  const totalPages = slides.length + 1;

  return (
    <div className="bg-white rounded-3xl p-6 md:p-8 border border-slate-100 shadow-sm space-y-6 relative overflow-hidden">
      <div className="flex flex-wrap items-center justify-between gap-4">
        <div className="flex items-center gap-3">
          <div className="w-10 h-10 rounded-2xl bg-blue-50 text-blue-600 font-extrabold flex items-center justify-center text-lg">{round.id}</div>
          <h4 className="text-lg font-bold text-slate-800">{round.stageName}</h4>
        </div>
        <div className="px-4 py-1.5 bg-blue-50/50 text-blue-600 rounded-full text-xs font-semibold border border-blue-100">阶段表现：{round.stageScore}分</div>
      </div>

      <div className="bg-slate-50/50 rounded-2xl p-5 border border-slate-100 space-y-5">

        {pptDetailPage > 0 && (
          <div className="flex items-center justify-end">
            <div className="flex items-center gap-2">
              <button onClick={() => setPptDetailPage(p => p - 1)} className="p-1 rounded-full border border-slate-200 bg-white hover:bg-slate-100 text-slate-500 transition">
                <ChevronLeft className="w-4 h-4" />
              </button>
              <span className="text-xs text-slate-400 font-mono">{pptDetailPage} / {slides.length}</span>
              <button onClick={() => { if (pptDetailPage < slides.length) setPptDetailPage(p => p + 1); }} disabled={pptDetailPage >= slides.length} className="p-1 rounded-full border border-slate-200 bg-white hover:bg-slate-100 text-slate-500 disabled:opacity-30 disabled:cursor-not-allowed transition">
                <ChevronRight className="w-4 h-4" />
              </button>
            </div>
          </div>
        )}

        {pptDetailPage === 0 ? (
          <div className="space-y-4">
            <div className="bg-white rounded-2xl p-5 border border-slate-100/80">
              <div className="flex items-center gap-2 mb-3">
                <div className="w-7 h-7 rounded-full bg-blue-50 flex items-center justify-center text-blue-500"><FileText className="w-4 h-4" /></div>
                <div>
                  <div className="text-xs font-bold text-slate-800">讲解课件</div>
                  <div className="text-[9px] text-slate-400">{selectedPPT.name}</div>
                </div>
              </div>
            </div>
            <div className="bg-white rounded-2xl p-4 border border-slate-100/80">
              <div className="flex items-center gap-2 text-blue-600 mb-2">
                <FileText className="w-4.5 h-4.5" />
                <span className="text-xs font-bold">整体建议总结</span>
              </div>
              <p className="text-xs text-slate-600 leading-relaxed">整体表现不错，没有口水词，突出关键信息。但需要注意 {worstThree.map((s, i) => (<span key={s.page}>{i > 0 && (i === worstThree.length - 1 ? '和' : '、')}<span className="font-bold text-amber-600">第{s.page}页</span></span>))} 的讲解得分较低，建议针对性加强。</p>
            </div>
            <div className="flex justify-center">
              <button onClick={() => setPptDetailPage(1)} className="px-6 py-2.5 bg-blue-600 hover:bg-blue-700 text-white font-bold rounded-full transition text-sm shadow-sm shadow-blue-100 flex items-center gap-2">
                <span>查看每一页PPT结果详情</span>
                <ChevronRight className="w-4 h-4" />
              </button>
            </div>
          </div>
        ) : (
          <div className="grid grid-cols-1 lg:grid-cols-2 gap-5">
            <div className="flex flex-col space-y-3">
              <span className="text-[10px] font-bold text-slate-400 uppercase">PPT 投影片缩略图</span>
              <div className="aspect-video bg-gradient-to-tr from-slate-900 to-slate-800 rounded-xl p-4 text-white flex flex-col justify-between shadow-inner flex-1">
                <div className="flex justify-between items-center text-[7px] opacity-60">
                  <span>{selectedPPT.name.substring(0, 10)}...</span>
                  <span>PAGE {slides[pptDetailPage - 1].page}</span>
                </div>
                <h4 className="text-xs font-bold text-white line-clamp-2 my-2 border-l-2 border-blue-500 pl-2">{slides[pptDetailPage - 1].title}</h4>
                <p className="text-[8px] text-slate-400 whitespace-pre-line">{slides[pptDetailPage - 1].content}</p>
              </div>
              <div className="bg-white p-3 rounded-xl border border-slate-200 flex items-center justify-between shadow-sm">
                <div><span className="text-[10px] text-slate-400 block">本页得分</span><span className="text-lg font-bold text-teal-600">{slides[pptDetailPage - 1].score}分</span></div>
                <span className="text-[9px] font-bold bg-teal-50 text-teal-600 px-2 py-0.5 rounded">多维度指标分析</span>
              </div>
            </div>
            <div className="flex flex-col space-y-3">
              <div className="bg-white rounded-xl p-4 border border-slate-100 shadow-sm">
                <span className="text-[10px] font-bold text-slate-400 tracking-wider block mb-2">标准答案说辞期望要点</span>
                <p className="text-xs text-slate-600 leading-relaxed">{slides[pptDetailPage - 1].standardAnswer}</p>
              </div>
              <div className="bg-white rounded-xl p-4 border border-slate-100 shadow-sm">
                <span className="text-[10px] font-bold text-blue-600 tracking-wider block mb-2">你实际回答内容（ASR转换）</span>
                <p className="text-xs text-slate-700 leading-relaxed bg-slate-50 p-2.5 rounded border border-slate-100">
                  {userPptAnswers[pptDetailPage - 1] ? `"${userPptAnswers[pptDetailPage - 1]}"` : <span className="text-slate-400 italic">"（本页未提供回答）"</span>}
                </p>
              </div>
              <div className="bg-slate-50 rounded-xl p-2.5 flex items-center gap-3 border border-slate-100">
                <button className="w-7 h-7 rounded-full bg-blue-500 hover:bg-blue-600 text-white flex items-center justify-center transition shrink-0">
                  <Play className="w-3.5 h-3.5 fill-current" />
                </button>
                <div className="flex-1 h-1.5 bg-slate-200 rounded-full relative">
                  <div className="absolute left-0 top-0 h-full w-0 bg-blue-500 rounded-full" />
                  <div className="absolute left-0 top-1/2 -translate-y-1/2 w-2.5 h-2.5 bg-white border border-blue-500 rounded-full shadow-sm" />
                </div>
                <span className="text-[9px] font-mono text-slate-400 shrink-0">0:00 / {slides[pptDetailPage - 1].score > 0 ? '2:' + String(slides[pptDetailPage - 1].score).padStart(2,'0') : '0:00'}</span>
              </div>
            </div>
          </div>
        )}
      </div>
    </div>
  );
}

function ResultPanel({ selectedPPT, userPptAnswers, qaQuestions, pptReviewSlideIndex, setPptReviewSlideIndex, isDetailOpen, setIsDetailOpen, setSimState, setActiveTab }) {
  const canvasRef = useRef(null);
  const [displayScore, setDisplayScore] = useState(0);
  const [pptDetailPage, setPptDetailPage] = useState(0); // 0=overview, 1..N=slide detail

  const generateReportData = () => {
    const rounds = qaQuestions.map((q, idx) => ({
      id: idx + 1,
      stageName: q.tag,
      stageScore: 0,
      questionNum: idx + 1,
      dimension: idx % 2 === 0 ? '产品介绍' : '逻辑表达',
      questionScore: 0,
      clientQuestion: q.fullText || q.question,
      myAnswer: '本题暂无现场回答',
      highScorePath: '系统将结合大数据模型生成最优回答路径，帮助您对标高分表达。',
      suggestion: '无',
      feedback: null
    }));

    if (selectedPPT) {
      rounds.splice(1, 0, {
        id: 2,
        stageName: '材料宣讲',
        stageScore: selectedPPT.slides.reduce((sum, s) => sum + s.score, 0) / selectedPPT.slides.length,
        questionNum: 2,
        dimension: 'PPT演讲',
        questionScore: Math.round(selectedPPT.slides.reduce((sum, s) => sum + s.score, 0) / selectedPPT.slides.length),
        clientQuestion: `PPT宣讲：${selectedPPT.name}（共${selectedPPT.slides.length}页）`,
        myAnswer: selectedPPT.slides.map(s => s.userAnswer).join('\n\n'),
        highScorePath: selectedPPT.slides.map(s => s.standardAnswer).join('\n\n'),
        suggestion: selectedPPT.slides.map(s => s.gapAnalysis).join('\n'),
        feedback: 'PPT讲解评测'
      });
      rounds.slice(2).forEach(r => { r.questionNum += 1; });
    }

    return rounds;
  };

  const reportData = generateReportData();

  const totalScore = selectedPPT
    ? Math.round(selectedPPT.slides.reduce((sum, s) => sum + s.score, 0) / selectedPPT.slides.length) + 5
    : 0;

  useEffect(() => {
    let current = 0;
    const step = Math.max(1, Math.floor(totalScore / 40));
    const timer = setInterval(() => {
      current += step;
      if (current >= totalScore) { setDisplayScore(totalScore); clearInterval(timer); }
      else { setDisplayScore(current); }
    }, 20);
    return () => clearInterval(timer);
  }, [totalScore]);

  useEffect(() => {
    const canvas = canvasRef.current;
    if (!canvas) return;
    const ctx = canvas.getContext('2d');
    const w = 256, h = 256, cx = 128, cy = 128;
    ctx.clearRect(0, 0, w, h);

    [45, 75, 105].forEach(r => {
      ctx.beginPath();
      ctx.strokeStyle = '#e2e8f0';
      ctx.lineWidth = 1;
      ctx.arc(cx, cy, r, 0, Math.PI * 2);
      ctx.stroke();
    });

    ctx.beginPath();
    ctx.strokeStyle = '#93c5fd';
    ctx.setLineDash([2, 4]);
    ctx.moveTo(cx, cy - 105);
    ctx.lineTo(cx, cy + 105);
    ctx.stroke();
    ctx.setLineDash([]);

    ctx.beginPath();
    ctx.arc(cx, cy, 4, 0, Math.PI * 2);
    ctx.fillStyle = '#3b82f6';
    ctx.fill();

    if (displayScore > 0) {
      const topY = cy - (displayScore / 100) * 105;
      const bottomY = cy + ((displayScore - 10 > 0 ? displayScore - 10 : 0) / 100) * 105;
      ctx.beginPath();
      ctx.strokeStyle = 'rgba(59, 130, 246, 0.7)';
      ctx.lineWidth = 3;
      ctx.moveTo(cx, topY);
      ctx.lineTo(cx, bottomY);
      ctx.stroke();
      ctx.fillStyle = '#3b82f6';
      ctx.beginPath();
      ctx.arc(cx, topY, 5, 0, Math.PI * 2);
      ctx.arc(cx, bottomY, 5, 0, Math.PI * 2);
      ctx.fill();
    }
  }, [displayScore]);

  return (
    <div className="max-w-5xl mx-auto space-y-8">
      <div className="bg-white rounded-3xl p-6 md:p-8 border border-slate-100 shadow-sm flex flex-col items-center">
        <h3 className="text-lg font-bold text-slate-800 mb-6">多维度能力测评图</h3>
        <div className="relative w-full max-w-md flex flex-col items-center py-4">
          <div className="relative w-64 h-64 flex items-center justify-center">
            <canvas ref={canvasRef} width={256} height={256} className="w-full h-full" />
            <div className="absolute -top-4 left-1/2 -translate-x-1/2 flex flex-col items-center">
              <div className="w-8 h-8 rounded-full bg-blue-50 flex items-center justify-center text-blue-500 mb-1 border border-blue-100">
                <Lightbulb className="w-4 h-4" />
              </div>
              <span className="text-xs font-semibold text-blue-600">产品介绍</span>
            </div>
            <div className="absolute -bottom-4 left-1/2 -translate-x-1/2 flex flex-col items-center">
              <div className="w-8 h-8 rounded-full bg-blue-50 flex items-center justify-center text-blue-500 mb-1 border border-blue-100">
                <User className="w-4 h-4" />
              </div>
              <span className="text-xs font-semibold text-blue-600">逻辑表达</span>
            </div>
          </div>
          <div className="w-full border-t border-dashed border-slate-200 mt-12 mb-4" />
          <div className="text-center">
            <div className="text-5xl font-black text-blue-600 tracking-tight flex items-baseline justify-center">
              <span>{displayScore}</span><span className="text-2xl font-bold ml-0.5">分</span>
            </div>
            <p className="text-sm font-medium text-slate-400 mt-1">综合表现评定</p>
          </div>
        </div>
      </div>

      <div className="flex flex-col md:flex-row md:items-center justify-between gap-4">
        <h3 className="text-xl font-bold text-slate-800">实战回合精细化对比</h3>
        <p className="text-slate-500 text-sm max-w-md">按业务推进阶段拆解客户问题、现场回答与推荐路径，帮助你快速定位高分打法与改进空间。</p>
      </div>

      <div className="space-y-8">
        {reportData.map((round) => (
          round.dimension === 'PPT演讲' ? (
            <PptRoundCard key={round.id} round={round} selectedPPT={selectedPPT} userPptAnswers={userPptAnswers} pptDetailPage={pptDetailPage} setPptDetailPage={setPptDetailPage} />
          ) : (
          <div key={round.id} className="bg-white rounded-3xl p-6 md:p-8 border border-slate-100 shadow-sm space-y-6">
            <div className="flex flex-wrap items-center justify-between gap-4">
              <div className="flex items-center gap-3">
                <div className="w-10 h-10 rounded-2xl bg-blue-50 text-blue-600 font-extrabold flex items-center justify-center text-lg">{round.id}</div>
                <h4 className="text-lg font-bold text-slate-800">{round.stageName}</h4>
              </div>
              <div className="px-4 py-1.5 bg-blue-50/50 text-blue-600 rounded-full text-xs font-semibold border border-blue-100">阶段表现：{round.stageScore}分</div>
            </div>

            <div className="bg-slate-50/50 rounded-2xl p-5 border border-slate-100 space-y-5">
              <div className="flex items-center justify-between">
                <div className="flex items-center gap-2">
                  <span className="px-2.5 py-0.5 bg-blue-600 text-white rounded-md text-[10px] font-bold">第 {round.questionNum} 题</span>
                  <span className="px-2.5 py-0.5 bg-slate-200 text-slate-600 rounded-md text-[10px] font-bold">{round.dimension}</span>
                </div>
                <div className="text-sm font-bold text-blue-600 bg-blue-50/70 px-3 py-1 rounded-full">{round.questionScore}分</div>
              </div>

              <div className="grid grid-cols-1 lg:grid-cols-3 gap-5">
                <div className="bg-white rounded-2xl p-5 border border-slate-100/80 flex flex-col">
                  <div className="flex items-center gap-2 mb-3">
                    <div className="w-7 h-7 rounded-full bg-blue-50 flex items-center justify-center text-blue-500"><User className="w-4 h-4" /></div>
                    <div>
                      <div className="text-xs font-bold text-slate-800">客户视角</div>
                      <div className="text-[9px] text-slate-400">客户提问内容</div>
                    </div>
                  </div>
                  <p className="text-xs text-slate-600 leading-relaxed flex-1">{round.clientQuestion}</p>
                </div>

                <div className="bg-white rounded-2xl p-5 border border-slate-100/80 flex flex-col min-h-[160px]">
                  <div className="flex items-center gap-2 mb-3">
                    <div className="w-7 h-7 rounded-full bg-emerald-50 flex items-center justify-center text-emerald-500"><MessageSquare className="w-4 h-4" /></div>
                    <div>
                      <div className="text-xs font-bold text-slate-800">现场作答</div>
                      <div className="text-[9px] text-slate-400">您的现场回答（TTS转录）</div>
                    </div>
                  </div>
                  <p className="text-xs text-slate-400 leading-relaxed italic flex-1">{round.myAnswer}</p>
                  <div className="mt-4 bg-slate-50 rounded-xl p-2.5 flex items-center gap-3 border border-slate-100">
                    <button className="w-7 h-7 rounded-full bg-blue-500 hover:bg-blue-600 text-white flex items-center justify-center transition shrink-0">
                      <Play className="w-3.5 h-3.5 fill-current" />
                    </button>
                    <div className="flex-1 h-1.5 bg-slate-200 rounded-full relative">
                      <div className="absolute left-0 top-0 h-full w-0 bg-blue-500 rounded-full" />
                      <div className="absolute left-0 top-1/2 -translate-y-1/2 w-2.5 h-2.5 bg-white border border-blue-500 rounded-full shadow-sm" />
                    </div>
                    <span className="text-[9px] font-mono text-slate-400 shrink-0">0:00 / 5:01</span>
                  </div>
                </div>

                <div className="bg-white rounded-2xl p-5 border border-slate-100/80 flex flex-col">
                  <div className="flex items-center gap-2 mb-3">
                    <div className="w-7 h-7 rounded-full bg-blue-50 flex items-center justify-center text-blue-500"><Navigation className="w-4 h-4" /></div>
                    <div>
                      <div className="text-xs font-bold text-slate-800">高分路径</div>
                      <div className="text-[9px] text-slate-400">系统推荐最优路径</div>
                    </div>
                  </div>
                  <p className="text-xs text-slate-600 leading-relaxed flex-1 whitespace-pre-line">{round.highScorePath}</p>
                </div>
              </div>

              <div className="bg-white rounded-2xl p-4 border border-slate-100/80">
                <div className="flex items-center gap-2 text-blue-600 mb-2">
                  <FileText className="w-4.5 h-4.5" />
                  <span className="text-xs font-bold">实战进阶建议</span>
                </div>
                <p className="text-xs text-slate-500 pl-6.5">{round.suggestion}</p>
              </div>

              {round.feedback && (
                <div className="flex items-center justify-between pt-2 border-t border-slate-100">
                  <span className="text-xs font-bold text-slate-700">本题反馈</span>
                </div>
              )}
            </div>
          </div>
          )
        ))}
      </div>

      {isDetailOpen && selectedPPT && (
        <div className="fixed inset-0 z-50 bg-black/60 backdrop-blur-sm flex items-center justify-center p-4">
          <div className="bg-white rounded-3xl shadow-2xl border border-slate-200 max-w-4xl w-full max-h-[90vh] flex flex-col overflow-hidden">
            <div className="p-6 border-b border-slate-100 flex justify-between items-center bg-slate-50/50">
              <div>
                <h3 className="text-base font-bold text-slate-800 flex items-center space-x-2">
                  <span className="bg-teal-600 text-white text-[10px] px-2 py-0.5 rounded">深度复盘详情</span>
                  <span>PPT 介绍逐页精细复盘分析</span>
                </h3>
                <p className="text-xs text-slate-400 mt-1">针对您演练讲解的《{selectedPPT.name}》各页，通过 ASR 提取进行差距评估</p>
              </div>
              <button onClick={() => setIsDetailOpen(false)} className="text-slate-400 hover:text-slate-600 p-1.5 rounded-full hover:bg-slate-100 transition-all"><X className="w-5 h-5" /></button>
            </div>
            <div className="p-6 flex-1 overflow-y-auto space-y-6">
              <div className="flex justify-between items-center bg-teal-50/50 border border-teal-100/60 p-3 rounded-xl mb-4">
                <span className="text-xs font-bold text-teal-800">PPT 单页详细评估</span>
                <div className="flex items-center space-x-3">
                  <span className="text-xs text-slate-500">当前载入: 第 <span className="font-bold text-slate-800">{pptReviewSlideIndex + 1}</span> / {selectedPPT.slides.length} 页</span>
                  <div className="flex space-x-1">
                    <button onClick={() => { if (pptReviewSlideIndex > 0) setPptReviewSlideIndex(prev => prev - 1); }} disabled={pptReviewSlideIndex === 0} className="p-1 px-2.5 rounded-lg border border-slate-200 bg-white hover:bg-slate-50 text-slate-600 disabled:opacity-40 text-xs font-semibold">上一页</button>
                    <button onClick={() => { if (pptReviewSlideIndex < selectedPPT.slides.length - 1) setPptReviewSlideIndex(prev => prev + 1); }} disabled={pptReviewSlideIndex === selectedPPT.slides.length - 1} className="p-1 px-2.5 rounded-lg border border-slate-200 bg-white hover:bg-slate-50 text-slate-600 disabled:opacity-40 text-xs font-semibold">下一页</button>
                  </div>
                </div>
              </div>
              <div className="grid grid-cols-1 md:grid-cols-12 gap-6 bg-slate-50 p-5 rounded-2xl border border-slate-200/40">
                <div className="md:col-span-4 flex flex-col justify-between space-y-4">
                  <div>
                    <span className="text-[9px] font-bold text-slate-400 block uppercase mb-1">PPT 投影片缩略图</span>
                    <div className="aspect-video bg-gradient-to-tr from-slate-900 to-slate-800 rounded-xl p-4 text-white flex flex-col justify-between shadow-inner">
                      <div className="flex justify-between items-center text-[7px] opacity-60"><span>制造业大厅数字改造</span><span>PAGE {selectedPPT.slides[pptReviewSlideIndex].page}</span></div>
                      <h4 className="text-[10px] font-bold text-white line-clamp-2 my-2 border-l-2 border-blue-500 pl-2">{selectedPPT.slides[pptReviewSlideIndex].title}</h4>
                      <p className="text-[7px] text-slate-400 line-clamp-2">{selectedPPT.slides[pptReviewSlideIndex].content}</p>
                    </div>
                  </div>
                  <div className="bg-white p-3 rounded-xl border border-slate-200 flex items-center justify-between shadow-sm">
                    <div><span className="text-[10px] text-slate-400 block">本页得分</span><span className="text-lg font-bold text-teal-600">{selectedPPT.slides[pptReviewSlideIndex].score}分</span></div>
                    <span className="text-[9px] font-bold bg-teal-50 text-teal-600 px-2 py-0.5 rounded">多维度指标分析完毕</span>
                  </div>
                </div>
                <div className="md:col-span-8 space-y-4">
                  <div className="grid grid-cols-1 sm:grid-cols-2 gap-4">
                    <div className="bg-white p-4 rounded-xl border border-slate-100 shadow-sm">
                      <span className="text-[10px] font-bold text-slate-400 tracking-wider block mb-2">标准答案说辞期望要点</span>
                      <p className="text-xs text-slate-600 leading-relaxed h-28 overflow-y-auto">{selectedPPT.slides[pptReviewSlideIndex].standardAnswer}</p>
                    </div>
                    <div className="bg-white p-4 rounded-xl border border-slate-100 shadow-sm">
                      <span className="text-[10px] font-bold text-blue-600 tracking-wider block mb-2">你实际回答内容 (ASR转换)</span>
                      <p className="text-xs text-slate-700 leading-relaxed font-mono h-28 overflow-y-auto bg-slate-50 p-2.5 rounded border border-slate-100">
                        {userPptAnswers[pptReviewSlideIndex] ? `"${userPptAnswers[pptReviewSlideIndex]}"` : <span className="text-slate-400 italic">"（本页未提供回答）"</span>}
                      </p>
                    </div>
                  </div>
                  <div className="bg-blue-50 border border-blue-100 p-4 rounded-xl">
                    <h4 className="text-xs font-bold text-blue-800 flex items-center space-x-1.5"><span className="w-1.5 h-1.5 bg-blue-600 rounded-full" /><span>差距总结建议</span></h4>
                    <p className="text-xs text-slate-600 leading-relaxed mt-2 pl-3">{selectedPPT.slides[pptReviewSlideIndex].gapAnalysis}</p>
                  </div>
                </div>
              </div>
            </div>
            <div className="p-4 bg-slate-50 border-t border-slate-100 text-right">
              <button onClick={() => setIsDetailOpen(false)} className="bg-slate-200 hover:bg-slate-300 text-slate-700 font-bold px-6 py-2 rounded-xl text-xs transition-all">关闭复盘</button>
            </div>
          </div>
        </div>
      )}
    </div>
  );
}

export default function App() {
  const [activeTab, setActiveTab] = useState('simulate');
  const [simState, setSimState] = useState('entry'); 
  const [sessionMode, setSessionMode] = useState(null);
  
  const [selectedPPT, setSelectedPPT] = useState(null);
  const [selectedPptId, setSelectedPptId] = useState(null); // Used for table radio selection
  
  const [currentSlideIndex, setCurrentSlideIndex] = useState(0);
  const [pptReviewSlideIndex, setPptReviewSlideIndex] = useState(0);
  const [isDetailOpen, setIsDetailOpen] = useState(false); 
  
  const [isPptPromptModalOpen, setIsPptPromptModalOpen] = useState(false);
  const [isVideoModalOpen, setIsVideoModalOpen] = useState(false);
  const [isPptSkipped, setIsPptSkipped] = useState(false);
  const [isRecording, setIsRecording] = useState(false);
  const [pptFinishStatus, setPptFinishStatus] = useState('completed'); // 'early' or 'completed'
  
  const [userPptAnswers, setUserPptAnswers] = useState(["", "", ""]);
  const [currentQaIndex, setCurrentQaIndex] = useState(0); 
  
  const qaQuestions = [
    { id: 1, tag: "环境破冰", question: "咱们先聊下，我听说你们有广交会的数据，能简单介绍一下吗？比如能不能查询往届的采购商信息？还有，能不能用产品关键词或者公司名称搜索呢？", fullText: "咱们先聊下，我听说你们有广交会的数据，能简单介绍一下吗？比如能不能查询往届的采购商信息？还有，能不能用产品关键词或者公司名称搜索呢？" },
    { id: 2, tag: "公司、产品核心价值传递", question: "能详细说说你们数字门户里的数字名片都有哪些主要功能吗？", fullText: "能详细说说你们数字门户里的数字名片都有哪些主要功能吗？" },
    { id: 3, tag: "公司、产品核心价值传递", question: "能具体介绍一下你们数字门户中的AI助手在内容创作方面都有哪些实用功能吗？", status: "已跳过" },
    { id: 4, tag: "公司、产品核心价值传递", question: "如果我使用你们数字门户的邮件营销工具，能通过哪些关键数据来评估营销效果呢？", status: "已跳过" },
    { id: 5, tag: "需求挖掘", question: "关于你们的门户网站，现在是如何管理和运营海外社交媒体的呢？比如，我能否直接在驾驶舱里用自然语言向AI提问，获取详细的指导？还有，在绑定Facebook主页时需要注意些什么吗？", status: "已跳过" },
    { id: 6, tag: "需求挖掘", question: "你们的门户网站后台能绑定多个运营平台吗，比如Twitter？发布的内容能不能在内容编辑页选择发布账号，实现同步到这些平台呢？", fullText: "你们的门户网站后台能绑定多个运营平台吗，比如Twitter？发布的内容能不能在内容编辑页选择发布账号，实现同步到这些平台呢？" }
  ];

  const [historyList, setHistoryList] = useState([
    { id: "9", path: "制造业 / 数字门户 / 专业型客户", pptName: "制造业数字门户2026核心解决方案.pdf", date: "2026-05-22 09:31", score: "85.0分", status: "已评测" },
    { id: "8", path: "制造业 / 数字门户 / 专业型客户", pptName: "无 (跳过演讲直接问答)", date: "2026-05-21 16:54", score: "0分", status: "未答完" },
    { id: "7", path: "制造业 / 数字门户 / 专业型客户", pptName: "数字渠道提效与客商在线白皮书.pdf", date: "2026-05-21 15:28", score: "1.5分", status: "未答完" },
    { id: "6", path: "制造业 / 数字门户 / 专业型客户", pptName: "无 (跳过演讲直接问答)", date: "2026-05-21 14:35", score: "15.4分", status: "已评测" }
  ]);

  const [isPlayingAudio, setIsPlayingAudio] = useState(false);
  const [audioText, setAudioText] = useState("");

  const triggerAudioPlay = (text, callback) => {
    setIsPlayingAudio(true);
    setAudioText(text);
    const timer = setTimeout(() => {
      setIsPlayingAudio(false);
      if (callback) callback();
    }, 4500);
    return () => clearTimeout(timer);
  };

  const resetSimSession = () => {
    setSessionMode(null);
    setCurrentQaIndex(0);
    setCurrentSlideIndex(0);
    setSelectedPPT(null);
    setSelectedPptId(null);
    setUserPptAnswers(["", "", ""]);
    setIsPlayingAudio(false);
    setAudioText("");
    setIsPptPromptModalOpen(false);
    setIsVideoModalOpen(false);
    setIsPptSkipped(false);
    setIsRecording(false);
  };

  const handleLaunchScenario = (mode) => {
    setSessionMode(mode);
    setSelectedPPT(null);
    setSelectedPptId(null);
    setCurrentSlideIndex(0);
    setUserPptAnswers(["", "", ""]);
    setIsPptSkipped(false);
    setIsRecording(false);

    if (mode === 'first_no_ppt' || mode === 'first_with_ppt') {
      setCurrentQaIndex(0);
      setSimState('prep');
      return;
    }

    if (mode === 'continue_before_ppt') {
      setCurrentQaIndex(0);
      setSimState('prep');
      return;
    }

    if (mode === 'continue_after_ppt') {
      setCurrentQaIndex(5);
      setSimState('qa');
    }
  };

  const handleStartSimChallenge = () => {
    if (sessionMode === 'continue_before_ppt') {
      setCurrentQaIndex(0);
      setSimState('icebreak');
      setIsPptPromptModalOpen(true);
      return;
    }
    setCurrentQaIndex(0);
    setSimState('icebreak');
  };

  const getPostPptQaIndex = () => (sessionMode === 'continue_after_ppt' ? 5 : 1);

  const handleFinishIcebreakAction = () => {
    if (sessionMode === 'first_no_ppt') {
      setCurrentQaIndex(1);
      setSimState('qa');
      return;
    }
    setIsPptPromptModalOpen(true);
  };

  const handleSkipPpt = () => {
    setIsPptPromptModalOpen(false);
    setIsPptSkipped(true);
    setCurrentQaIndex(getPostPptQaIndex());
    setSimState('qa');
  };

  const handleEnterPpt = () => {
    setIsPptPromptModalOpen(false);
    setSimState('ppt_select');
  };

  const handleDirectExam = () => {
    const ppt = PPT_LIST.find(p => p.id === selectedPptId);
    setSelectedPPT(ppt);
    setCurrentSlideIndex(0);
    setSimState('ppt_presenting');
  };

  const handleNextSlide = () => {
    if (currentSlideIndex < selectedPPT.slides.length - 1) {
      setCurrentSlideIndex(prev => prev + 1);
    } else {
      setPptFinishStatus('completed');
      setSimState('transition_to_qa');
      triggerAudioPlay("感谢你的介绍，我已经差不多了解了，还有一些问题想和你确认。", () => {
        setCurrentQaIndex(getPostPptQaIndex());
        setSimState('qa');
      });
    }
  };

  const handleEarlyClosePpt = () => {
    setPptFinishStatus('early');
    setSimState('transition_to_qa');
    triggerAudioPlay("好吧，听了你的ppt我还是有很多疑惑。", () => {
      setCurrentQaIndex(getPostPptQaIndex());
      setSimState('qa');
    });
  };

  const handleFinishQa = () => {
    if (currentQaIndex < qaQuestions.length - 1) {
      setCurrentQaIndex((prev) => prev + 1);
      return;
    }

    setActiveTab('result');
    const newRecord = {
      id: (historyList.length + 6).toString(),
      path: "制造业 / 数字门户 / 专业型客户",
      pptName: selectedPPT ? selectedPPT.name : "无 (未宣讲)",
      date: new Date().toISOString().slice(0, 16).replace('T', ' '),
      score: "85.2分",
      status: "已评测"
    };
    setHistoryList([newRecord, ...historyList]);
  };

  const hasMaterialStage = ['first_with_ppt', 'continue_before_ppt', 'continue_after_ppt'].includes(sessionMode);
  const totalSessionSteps = hasMaterialStage ? 11 : 10;

  const buildSessionTimeline = () => {
    const items = [
      { key: 'icebreak', stepLabel: '问题 1', tag: '环境破冰', content: qaQuestions[0].question, type: 'icebreak' },
    ];

    if (hasMaterialStage) {
      items.push({
        key: 'ppt',
        stepLabel: '阶段 2',
        tag: '材料宣讲',
        content: selectedPPT ? selectedPPT.name : "请选择要讲授的材料",
        type: 'ppt',
      });
    }

    qaQuestions.slice(1).forEach((q, idx) => {
      items.push({
        key: `qa-${q.id}`,
        stepLabel: `问题 ${hasMaterialStage ? idx + 3 : idx + 2}`,
        tag: q.tag,
        content: q.question,
        type: 'qa',
      });
    });

    return items;
  };

  const getActiveTimelineKey = () => {
    if (simState === 'icebreak') return 'icebreak';
    if (simState === 'ppt_select' || simState === 'ppt_presenting') {
      return hasMaterialStage ? 'ppt' : 'icebreak';
    }
    if (simState === 'qa' || simState === 'transition_to_qa') {
      return `qa-${qaQuestions[currentQaIndex]?.id || 1}`;
    }
    return 'icebreak';
  };

  const sessionTimeline = buildSessionTimeline();
  const activeTimelineKey = getActiveTimelineKey();
  const activeTimelineIndex = sessionTimeline.findIndex((item) => item.key === activeTimelineKey);
  const currentStepNumber = activeTimelineIndex >= 0 ? activeTimelineIndex + 1 : 1;
  const sessionProgress = Math.round((currentStepNumber / totalSessionSteps) * 100);

  const getTimelineItemStatus = (item, index) => {
    if (index === activeTimelineIndex) {
      if (item.type === 'ppt' || item.type === 'icebreak') return '进行中';
      return '待回答';
    }
    if (index < activeTimelineIndex) {
      if (item.type === 'ppt') return isPptSkipped ? '已跳过' : '已完成';
      return '已完成';
    }
    return item.type === 'ppt' ? '待开始' : '已跳过';
  };

  const renderSessionProgressHeader = () => (
    <div className="flex items-center space-x-4">
      <span className="text-xs font-bold text-blue-600 bg-blue-50 px-2 py-0.5 rounded">
        当前第 {currentStepNumber}/{totalSessionSteps} 步
      </span>
      <div className="w-24 bg-slate-100 h-1.5 rounded-full overflow-hidden">
        <div className="bg-blue-500 h-full" style={{ width: `${sessionProgress}%` }}></div>
      </div>
      <span className="text-xs text-slate-400">{sessionProgress}%</span>
    </div>
  );

  const renderSessionHistory = () => (
    <div className="lg:col-span-4 bg-white rounded-2xl border border-slate-200/80 shadow-sm p-4 flex flex-col overflow-hidden h-full">
      <div className="border-b border-slate-100 pb-3 mb-3 flex items-center space-x-1.5 text-slate-700">
        <MessageSquare className="w-4 h-4 text-blue-500" />
        <h3 className="text-xs font-bold uppercase tracking-wider">问答历史</h3>
      </div>

      <div className="flex-1 space-y-3 overflow-y-auto pr-1">
        {sessionTimeline.map((item, index) => {
          const isActive = item.key === activeTimelineKey;
          const statusText = getTimelineItemStatus(item, index);

          return (
            <div
              key={item.key}
              className={`p-3 rounded-xl border text-xs relative ${
                isActive ? 'border-blue-500 bg-blue-50/20' : 'border-slate-100 bg-[#FAFBFD]/60 opacity-75'
              }`}
            >
              {isActive && (
                <div className="absolute -left-1 top-1/2 -translate-y-1/2 w-2 h-4 bg-blue-500 rounded-r-md"></div>
              )}
              <div className="flex justify-between items-center mb-1">
                <span className={`font-bold flex items-center ${isActive ? 'text-slate-800' : 'text-slate-700'}`}>
                  {item.stepLabel}
                  {isActive && <span className="text-red-500 ml-1">←</span>}
                </span>
                <span className={`text-[9px] px-1.5 py-0.5 rounded font-bold ${isActive ? 'bg-blue-100 text-blue-700' : 'bg-slate-100 text-slate-500'}`}>
                  {item.tag}
                </span>
              </div>
              <p className="text-slate-500 line-clamp-2 text-[10px] leading-relaxed">{item.content}</p>
              <span className={`text-[9px] font-semibold block mt-1.5 ${statusText === '已跳过' ? 'text-amber-500' : isActive ? 'text-blue-600' : 'text-emerald-600'}`}>
                {statusText}
              </span>
            </div>
          );
        })}
      </div>
    </div>
  );

  const drillSteps = (sessionMode === 'first_with_ppt' || sessionMode === 'continue_before_ppt') ? DRILL_STEPS_WITH_PPT : DRILL_STEPS_NO_PPT;
  const currentQuestion = qaQuestions[currentQaIndex];
  const questionDisplayText = currentQuestion?.fullText || currentQuestion?.question;

  return (
    <div className="flex h-screen bg-[#F4F7FC] text-slate-800 font-sans overflow-hidden">
      
      {/* PPT Prompt Modal Before Entering List */}
      {isPptPromptModalOpen && simState !== 'prep' && (
        <div className="fixed inset-0 z-[60] bg-black/50 backdrop-blur-sm flex items-center justify-center p-4">
          <div className="bg-white rounded-2xl shadow-2xl border border-slate-200 w-[420px] overflow-hidden transform transition-all scale-100 opacity-100">
            <div className="bg-blue-600 p-5 text-center text-white relative">
              <FileText className="w-12 h-12 mx-auto opacity-90 mb-2" />
              <h3 className="text-lg font-bold tracking-wider">进入材料宣讲环节？</h3>
              <p className="text-xs text-blue-100 mt-1">您可以选择讲授课件或直接跳过此阶段进入追问</p>
            </div>
            <div className="p-6 bg-slate-50 flex space-x-3">
              <button 
                onClick={handleSkipPpt}
                className="flex-1 py-3 px-4 bg-white border border-slate-200 text-slate-600 hover:bg-slate-100 font-bold rounded-xl transition-all shadow-sm text-sm"
              >
                跳过此环节
              </button>
              <button 
                onClick={handleEnterPpt}
                className="flex-1 py-3 px-4 bg-blue-600 border border-blue-600 text-white hover:bg-blue-700 font-bold rounded-xl transition-all shadow-md shadow-blue-100 text-sm"
              >
                进入材料宣讲
              </button>
            </div>
          </div>
        </div>
      )}

      {/* PPT Learn Video Modal */}
      {isVideoModalOpen && (
        <div className="fixed inset-0 z-[60] bg-black/60 backdrop-blur-sm flex items-center justify-center p-4">
          <div className="bg-white rounded-2xl shadow-2xl w-full max-w-4xl overflow-hidden flex flex-col">
            <div className="p-4 border-b border-slate-100 flex justify-between items-center bg-slate-50">
              <h3 className="font-bold text-slate-800 flex items-center space-x-2">
                <Video className="w-5 h-5 text-indigo-600" />
                <span>PPT 微课学习：{PPT_LIST.find(p => p.id === selectedPptId)?.name}</span>
              </h3>
              <button onClick={() => setIsVideoModalOpen(false)} className="text-slate-400 hover:text-slate-600 p-1 rounded-full hover:bg-slate-200 transition-all">
                <X className="w-5 h-5" />
              </button>
            </div>
            <div className="aspect-video bg-black flex items-center justify-center relative">
              <Play className="w-16 h-16 text-white/50 absolute" />
              <div className="absolute inset-0 bg-[url('https://images.unsplash.com/photo-1516321497487-e288fb19713f?auto=format&fit=crop&q=80&w=1000')] bg-cover bg-center opacity-30"></div>
              <span className="text-white relative z-10 font-bold tracking-widest opacity-80">视频模拟加载中...</span>
            </div>
            <div className="p-4 bg-slate-50 flex justify-end space-x-3 border-t border-slate-100">
              <button 
                onClick={() => setIsVideoModalOpen(false)}
                className="px-6 py-2.5 bg-white border border-slate-200 text-slate-600 font-bold rounded-lg transition-all hover:bg-slate-100"
              >
                关闭视频
              </button>
              <button 
                onClick={() => { setIsVideoModalOpen(false); handleDirectExam(); }}
                className="px-6 py-2.5 bg-blue-600 text-white font-bold rounded-lg transition-all hover:bg-blue-700 shadow-sm"
              >
                前往考试
              </button>
            </div>
          </div>
        </div>
      )}

      {/* LEFT SIDEBAR */}
      <div className="w-64 bg-white border-r border-slate-200 flex flex-col justify-between z-10">
        <div>
          <div className="p-6 border-b border-slate-100 flex items-center space-x-3">
            <div className="w-8 h-8 bg-blue-600 rounded-lg flex items-center justify-center text-white font-bold text-lg shadow-md shadow-blue-200">领</div>
            <div>
              <h1 className="font-bold text-slate-800 tracking-wide text-base">领航者</h1>
              <p className="text-xs text-slate-400">销售训练工作台</p>
            </div>
          </div>
          <nav className="p-4 space-y-1">
            <button 
              onClick={() => { setActiveTab('simulate'); resetSimSession(); setSimState('entry'); }} 
              className={`w-full flex items-center space-x-3 px-4 py-3 rounded-xl text-sm font-medium transition-all ${activeTab === 'simulate' ? 'bg-blue-50 text-blue-600 shadow-sm' : 'text-slate-600 hover:bg-slate-50 hover:text-slate-900'}`}
            >
              <Tv className="w-5 h-5" />
              <span>模拟实战</span>
            </button>
            <button 
              onClick={() => { setActiveTab('history'); }} 
              className={`w-full flex items-center space-x-3 px-4 py-3 rounded-xl text-sm font-medium transition-all ${activeTab === 'history' ? 'bg-blue-50 text-blue-600 shadow-sm' : 'text-slate-600 hover:bg-slate-50 hover:text-slate-900'}`}
            >
              <History className="w-5 h-5" />
              <span>历史记录</span>
            </button>
          </nav>
        </div>
        <div className="p-4 border-t border-slate-100 bg-slate-50/50">
          <div className="flex items-center space-x-3 p-2 bg-white rounded-xl shadow-sm border border-slate-100">
            <div className="w-10 h-10 rounded-full bg-gradient-to-tr from-blue-500 to-indigo-600 text-white flex items-center justify-center font-bold text-sm">苏</div>
            <div className="overflow-hidden">
              <h4 className="text-sm font-bold text-slate-800 truncate">苏晓莹</h4>
              <p className="text-xs text-slate-400 truncate">功能测试工程师</p>
            </div>
          </div>
        </div>
      </div>

      {/* MAIN CONTAINER */}
      <div className="flex-1 flex flex-col overflow-hidden relative">
        <header className="bg-white h-14 border-b border-slate-200 px-6 flex items-center justify-between z-10">
          <div className="flex items-center space-x-3">
            <span className="text-xs font-semibold px-2.5 py-1 bg-slate-100 text-slate-600 rounded-md">实战测评</span>
            <span className="text-slate-300">/</span>
            <span className="text-sm text-slate-700 font-medium">制造业 · 数字门户 · 专业型客户</span>
          </div>
          <div className="flex items-center space-x-4">
            <div className="flex items-center space-x-2 text-xs text-slate-400">
              <span className="inline-block w-2.5 h-2.5 bg-green-500 rounded-full animate-pulse"></span>
              <span>系统运行正常</span>
            </div>
            <button 
              onClick={() => { resetSimSession(); setSimState('entry'); setActiveTab('simulate'); }}
              className="text-xs bg-slate-100 hover:bg-slate-200 text-slate-600 font-medium px-3 py-1.5 rounded-lg transition-all"
            >
              重新启动
            </button>
          </div>
        </header>

        <div className="flex-1 overflow-y-auto p-6 relative">
          
          {/* ======================= TAB: SIMULATE ======================= */}
          {activeTab === 'simulate' && (
            <div className="h-full max-w-7xl mx-auto flex flex-col justify-between relative">
              
              {/* STATE 0: INITIAL STARTING SCREEN */}
              {(simState === 'entry' || simState === 'prep') && (
                <div className="flex-1 flex flex-col justify-between h-full">
                  <div className="bg-blue-600 rounded-2xl p-5 mb-6 text-white flex flex-col md:flex-row md:items-center justify-between shadow-md shadow-blue-100">
                    <div>
                      <h2 className="text-base font-bold">选择客户类型测评</h2>
                      <p className="text-xs opacity-80 mt-0.5">请选择您想要挑战的客户类型，进行对战练习，加油！🚀</p>
                    </div>
                    <div className="flex space-x-2 mt-3 md:mt-0">
                      <span className="bg-white/15 px-3 py-1 rounded-full text-xs font-medium">制造业</span>
                      <span className="bg-white/15 px-3 py-1 rounded-full text-xs font-medium">数字门户</span>
                    </div>
                  </div>

                  {simState === 'entry' && (
                    <>
                      <div className="flex-1 space-y-6 py-4 overflow-y-auto">
                        {DEMO_SCENARIOS.map((scenario) => (
                          <div key={scenario.id} className="bg-white rounded-2xl p-8 border border-slate-200/80 shadow-lg max-w-2xl w-full mx-auto relative overflow-hidden">
                            <div className="absolute right-8 top-4 text-slate-100/70 font-black text-8xl tracking-tighter select-none pointer-events-none">{scenario.cardNo}</div>
                            <div className="flex items-center space-x-2 mb-4">
                              <div className="w-2.5 h-5 bg-blue-600 rounded-sm"></div>
                              <h3 className="text-xl font-bold text-slate-800">{CLIENT_CARD.title}</h3>
                            </div>
                            <p className="text-sm text-slate-500 leading-relaxed mb-8 pr-12">{CLIENT_CARD.description}</p>
                            <div className="flex flex-col sm:flex-row sm:items-center space-y-3 sm:space-y-0 sm:space-x-4">
                              <button onClick={() => handleLaunchScenario(scenario.id)} className="flex-1 bg-blue-600 hover:bg-blue-700 text-white font-bold py-3.5 px-6 rounded-xl transition-all shadow-md shadow-blue-100 flex items-center justify-center">
                                <span>{scenario.actionLabel}</span>
                              </button>
                              <button onClick={() => setActiveTab('result')} className="flex-1 bg-slate-50 hover:bg-slate-100 border border-slate-200 text-slate-600 font-bold py-3.5 px-6 rounded-xl transition-all flex items-center justify-center">
                                <span>查看结果</span>
                              </button>
                            </div>
                          </div>
                        ))}
                      </div>
                      <div className="pt-4 border-t border-slate-100 flex justify-between items-center text-xs text-slate-400">
                        <span>第 1-{DEMO_SCENARIOS.length} 条，共 {DEMO_SCENARIOS.length} 条</span>
                        <div className="flex space-x-1">
                          <button className="px-3 py-1 rounded border border-slate-100 bg-white hover:bg-slate-50 text-slate-400" disabled>上一页</button>
                          <button className="px-3 py-1 rounded bg-blue-600 text-white font-bold">1</button>
                          <button className="px-3 py-1 rounded border border-slate-100 bg-white hover:bg-slate-50 text-slate-400" disabled>下一页</button>
                        </div>
                      </div>
                    </>
                  )}

                  {simState === 'prep' && (
                    <div className="fixed inset-0 z-50 bg-black/60 backdrop-blur-sm flex items-center justify-center p-4">
                      <div className="bg-[#FAFBFD] rounded-3xl shadow-2xl border border-slate-200 max-w-5xl w-full max-h-[92vh] flex flex-col overflow-hidden relative">
                        <div className="absolute top-0 left-1/2 -translate-x-1/2 -translate-y-1/2 z-10">
                          <span className="bg-blue-50 text-blue-600 border border-blue-200 text-xs font-bold px-4 py-1.5 rounded-full shadow-sm tracking-wider">
                            {sessionMode === 'first_no_ppt' ? '无材料宣讲演练背景' : '实战演练背景'}
                          </span>
                        </div>
                        <button onClick={() => { resetSimSession(); setSimState('entry'); }} className="absolute top-4 right-4 text-slate-400 hover:text-slate-600 p-1.5 rounded-full hover:bg-slate-100 transition-all z-10">
                          <X className="w-5 h-5" />
                        </button>
                        <div className="text-center pt-8 pb-4">
                          <h2 className="text-xl font-bold text-slate-800 tracking-tight">【制造业】客户需求实战训练</h2>
                          <p className="text-xs text-slate-400 mt-1">聚焦【数字门户】的核心应用 · 专业型客户</p>
                        </div>
                        <div className="px-8 pb-6 flex-1 overflow-y-auto space-y-6">
                          <div className="grid grid-cols-1 md:grid-cols-12 gap-6">
                            <div className="md:col-span-5 bg-white rounded-2xl p-5 border border-slate-200/60 shadow-sm flex flex-col space-y-4">
                              <div className="flex items-center space-x-2 text-blue-600">
                                <User className="w-5 h-5" />
                                <h3 className="font-bold text-slate-800 text-xs tracking-wider">Agent 角色设定</h3>
                              </div>
                              <div>
                                <span className="text-[10px] text-slate-400 font-semibold block uppercase tracking-wider">扮演角色</span>
                                <span className="text-xs font-bold text-slate-700 mt-1 inline-block">一名 【专业型客户】 客户</span>
                              </div>
                              <div>
                                <span className="text-[10px] text-slate-400 font-semibold block uppercase tracking-wider">客户特征</span>
                                <p className="text-xs text-slate-500 leading-relaxed mt-1 bg-slate-50 p-3 rounded-xl border border-slate-100">{CLIENT_CARD.description}</p>
                              </div>
                            </div>
                            <div className="md:col-span-7 space-y-4 flex flex-col justify-between">
                              <div className="bg-white rounded-2xl p-5 border border-slate-200/60 shadow-sm flex-1 flex flex-col justify-center space-y-2">
                                <div className="flex items-center space-x-2 text-indigo-600">
                                  <FileText className="w-5 h-5" />
                                  <h3 className="font-bold text-slate-800 text-xs tracking-wider">场景介绍</h3>
                                </div>
                                <p className="text-xs text-slate-500 leading-relaxed pl-1">考核数字门户的核心功能及其对运营效率的提升。</p>
                              </div>
                              <div className="bg-white rounded-2xl p-5 border border-slate-200/60 shadow-sm flex-1 flex flex-col justify-center space-y-2">
                                <div className="flex items-center space-x-2 text-emerald-600">
                                  <Compass className="w-5 h-5" />
                                  <h3 className="font-bold text-slate-800 text-xs tracking-wider">对话目标</h3>
                                </div>
                                <p className="text-xs text-slate-500 leading-relaxed pl-1">围绕「制造业-数字门户-专业型客户」完成结构化表达。</p>
                              </div>
                            </div>
                          </div>
                          <div className="bg-white rounded-2xl p-5 border border-slate-200/60 shadow-sm">
                            <div className="flex items-center space-x-2 text-indigo-600 mb-4">
                              <div className="w-1 h-3 bg-indigo-600 rounded"></div>
                              <h3 className="font-bold text-slate-800 text-xs tracking-wider">演练环节安排</h3>
                            </div>
                            <div className={`grid grid-cols-1 gap-4 ${drillSteps.length > 4 ? 'sm:grid-cols-2 lg:grid-cols-5' : 'sm:grid-cols-2 lg:grid-cols-4'}`}>
                              {drillSteps.map((step) => (
                                <div key={step.title} className="bg-slate-50 rounded-xl p-4 border border-slate-100 flex flex-col space-y-1">
                                  <h4 className="text-xs font-bold text-slate-700">{step.title}</h4>
                                  <p className="text-[10px] text-slate-400 leading-relaxed">{step.desc}</p>
                                </div>
                              ))}
                            </div>
                          </div>
                        </div>
                        <div className="p-6 bg-slate-50 border-t border-slate-100 flex flex-col sm:flex-row sm:items-center justify-between gap-4">
                          <div className="flex items-start space-x-2 max-w-lg">
                            <AlertCircle className="w-5 h-5 text-amber-500 flex-shrink-0 mt-0.5" />
                            <div>
                              <span className="text-[11px] font-bold text-amber-700 block">沟通指南</span>
                              <p className="text-[10px] text-slate-500 mt-0.5 leading-relaxed">本次实战中，学员共有 <span className="underline font-bold text-amber-800">3次提示机会</span> 可使用。建议围绕核心话术库展开。</p>
                            </div>
                          </div>
                          <button onClick={handleStartSimChallenge} className="bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 px-8 rounded-xl transition-all shadow-lg shadow-blue-100 text-sm flex items-center space-x-1.5">
                            <span>开启实战挑战</span>
                            <ChevronRight className="w-4 h-4" />
                          </button>
                        </div>
                      </div>
                    </div>
                  )}

                  {isPptPromptModalOpen && simState === 'prep' && (
                    <div className="fixed inset-0 z-[65] bg-black/70 backdrop-blur-sm flex items-center justify-center p-4">
                      <div className="bg-white rounded-2xl shadow-2xl border border-slate-200 w-[420px] overflow-hidden transform transition-all scale-100 opacity-100">
                        <div className="bg-blue-600 p-5 text-center text-white relative">
                          <FileText className="w-12 h-12 mx-auto opacity-90 mb-2" />
                          <h3 className="text-lg font-bold tracking-wider">进入材料宣讲环节？</h3>
                          <p className="text-xs text-blue-100 mt-1">您可以选择讲授课件或直接跳过此阶段进入追问</p>
                        </div>
                        <div className="p-6 bg-slate-50 flex space-x-3">
                          <button 
                            onClick={handleSkipPpt}
                            className="flex-1 py-3 px-4 bg-white border border-slate-200 text-slate-600 hover:bg-slate-100 font-bold rounded-xl transition-all shadow-sm text-sm"
                          >
                            跳过此环节
                          </button>
                          <button 
                            onClick={handleEnterPpt}
                            className="flex-1 py-3 px-4 bg-blue-600 border border-blue-600 text-white hover:bg-blue-700 font-bold rounded-xl transition-all shadow-md shadow-blue-100 text-sm"
                          >
                            进入材料宣讲
                          </button>
                        </div>
                      </div>
                    </div>
                  )}
                </div>
              )}

              {/* STATE 2: ENVIRONMENT ICEBREAK */}
              {simState === 'icebreak' && (
                <div className="bg-white rounded-2xl shadow-sm border border-slate-200 flex-1 flex flex-col overflow-hidden h-full">
                  <div className="bg-white border-b border-slate-100 px-6 py-3 flex items-center justify-between">
                    <div className="flex items-center space-x-2 text-xs font-semibold text-slate-600">
                      <span className="text-slate-400">实战测评 · 制造业 · 数字门户 · 专业型客户</span>
                    </div>
                    <div className="flex items-center space-x-4">{renderSessionProgressHeader()}</div>
                  </div>
                  <div className="flex-1 grid grid-cols-1 lg:grid-cols-12 gap-5 p-5 bg-[#F8FAFC]">
                    <div className="lg:col-span-4 bg-white rounded-2xl border border-slate-200/80 shadow-sm p-4 flex flex-col justify-between">
                      <div className="flex-1 flex items-center justify-center py-4"><AnimeAvatar /></div>
                      <div className="bg-[#FAFBFD] p-4 rounded-2xl border border-blue-100 relative shadow-sm">
                        <div className="absolute -top-2 left-1/2 transform -translate-x-1/2 w-4 h-4 bg-[#FAFBFD] rotate-45 border-t border-l border-blue-100"></div>
                        <div className="flex items-center justify-between mb-2">
                          <span className="text-[10px] bg-green-100 text-green-700 font-bold px-2 py-0.5 rounded-full flex items-center space-x-1">
                            <span className="w-1.5 h-1.5 bg-green-500 rounded-full animate-pulse"></span>
                            <span>正在录音</span>
                          </span>
                          <span className="text-[10px] text-blue-600 bg-blue-50 px-2 py-0.5 rounded font-bold">环境破冰</span>
                        </div>
                        <p className="text-xs text-slate-700 leading-relaxed font-medium">{qaQuestions[currentQaIndex]?.fullText}</p>
                      </div>
                    </div>
                    <div className="lg:col-span-4 flex flex-col justify-between bg-white rounded-2xl border border-slate-200/80 shadow-sm p-5">
                      <div>
                        <div className="aspect-square bg-slate-950 rounded-2xl relative overflow-hidden shadow-inner border border-slate-900 flex items-center justify-center">
                          <div className="absolute inset-0 bg-[url('https://images.unsplash.com/photo-1502082553048-f009c37129b9?auto=format&fit=crop&q=80&w=600')] bg-cover bg-center opacity-60"></div>
                          <div className="absolute top-3 right-3 bg-blue-600 text-white text-[10px] font-bold px-2 py-0.5 rounded-md flex items-center space-x-1 shadow-sm">
                            <span className="w-1.5 h-1.5 bg-white rounded-full animate-ping"></span>
                            <span>REC</span>
                          </div>
                          <div className="absolute bottom-3 left-3 bg-black/50 text-white text-[9px] px-2 py-0.5 rounded">麦克风：内置通道 3</div>
                        </div>
                      </div>
                      <div className="my-4 text-center">
                        <div className="inline-block bg-slate-50 border border-slate-100 rounded-2xl px-6 py-2 shadow-sm">
                          <div className="flex items-center justify-center space-x-1.5 text-slate-400">
                            <Clock className="w-3.5 h-3.5 text-blue-500" />
                            <span className="text-[10px] font-bold tracking-wider">剩余时间</span>
                          </div>
                          <span className="text-2xl font-black text-blue-600 tracking-tight block mt-0.5">04:45</span>
                        </div>
                      </div>
                      <div className="space-y-4">
                        <button onClick={handleFinishIcebreakAction} className="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-3.5 px-6 rounded-2xl transition-all shadow-md shadow-blue-100 tracking-wider text-sm text-center block">
                          结束回答
                        </button>
                        <div className="grid grid-cols-3 gap-2">
                          <button className="flex flex-col items-center justify-center py-2 bg-slate-50 hover:bg-slate-100 border border-slate-200/50 rounded-xl transition-all text-slate-600">
                            <Sparkles className="w-4 h-4 text-amber-500 mb-1" />
                            <span className="text-[10px] font-bold">战术锦囊</span>
                          </button>
                          <button className="flex flex-col items-center justify-center py-2 bg-slate-50 hover:bg-slate-100 border border-slate-200/50 rounded-xl transition-all text-slate-600">
                            <RotateCcw className="w-4 h-4 text-blue-500 mb-1" />
                            <span className="text-[10px] font-bold">重新回答</span>
                          </button>
                          <button onClick={handleFinishIcebreakAction} className="flex flex-col items-center justify-center py-2 bg-slate-50 hover:bg-slate-100 border border-slate-200/50 rounded-xl transition-all text-slate-600">
                            <ChevronRight className="w-4 h-4 text-slate-500 mb-1" />
                            <span className="text-[10px] font-bold">跳过此题</span>
                          </button>
                        </div>
                      </div>
                    </div>
                    {renderSessionHistory()}
                  </div>
                </div>
              )}

              {/* STATE 4: PPT SELECT LIST (REFactored to Table List) */}
              {simState === 'ppt_select' && (
                <div className="bg-white rounded-2xl shadow-sm border border-slate-200 flex-1 flex flex-col overflow-hidden h-full">
                  <div className="p-6 border-b border-slate-100 flex justify-between items-center bg-slate-50/50">
                    <div>
                      <h2 className="text-lg font-bold text-slate-800">请选择您想要讲的 PPT 资料</h2>
                      <p className="text-xs text-slate-400 mt-0.5">请在列表中选择一个PPT素材，然后点击直接考试或先学习。</p>
                    </div>
                    <span className="text-xs text-slate-400 font-medium">可用 PPT：{PPT_LIST.length} 套</span>
                  </div>

                  <div className="flex-1 overflow-y-auto p-6">
                    <table className="w-full text-left text-sm border-collapse rounded-xl overflow-hidden shadow-sm border border-slate-200">
                      <thead className="bg-slate-50 border-b border-slate-200 text-slate-500">
                        <tr>
                          <th className="p-4 font-semibold w-16 text-center">选择</th>
                          <th className="p-4 font-semibold">PPT 名称</th>
                          <th className="p-4 font-semibold w-48">上传日期</th>
                          <th className="p-4 font-semibold w-32">考试状态</th>
                        </tr>
                      </thead>
                      <tbody className="divide-y divide-slate-100">
                        {PPT_LIST.map((ppt) => (
                          <tr 
                            key={ppt.id} 
                            onClick={() => setSelectedPptId(ppt.id)}
                            className={`cursor-pointer transition-colors ${selectedPptId === ppt.id ? 'bg-blue-50/60' : 'hover:bg-slate-50'}`}
                          >
                            <td className="p-4 text-center">
                              <input 
                                type="radio" 
                                name="pptSelection"
                                className="w-4 h-4 text-blue-600 focus:ring-blue-500 cursor-pointer border-slate-300"
                                checked={selectedPptId === ppt.id}
                                onChange={() => setSelectedPptId(ppt.id)}
                              />
                            </td>
                            <td className="p-4 font-medium text-slate-700 flex items-center space-x-2.5">
                              <div className="w-8 h-8 rounded bg-indigo-50 flex items-center justify-center text-indigo-500">
                                <FileText className="w-4 h-4" />
                              </div>
                              <span className={selectedPptId === ppt.id ? 'text-blue-700 font-bold' : ''}>{ppt.name}</span>
                            </td>
                            <td className="p-4 text-slate-500 text-xs">{ppt.uploadDate}</td>
                            <td className="p-4">
                              {ppt.isExamined ? (
                                <span className="bg-green-100/70 text-green-700 border border-green-200 px-2.5 py-1 rounded text-xs font-bold flex items-center w-max space-x-1">
                                  <CheckCircle2 className="w-3 h-3" />
                                  <span>已考试</span>
                                </span>
                              ) : (
                                <span className="bg-slate-100 text-slate-500 border border-slate-200 px-2.5 py-1 rounded text-xs font-bold flex items-center w-max space-x-1">
                                  <Clock className="w-3 h-3" />
                                  <span>未考试</span>
                                </span>
                              )}
                            </td>
                          </tr>
                        ))}
                      </tbody>
                    </table>
                  </div>

                  <div className="p-5 bg-slate-50 border-t border-slate-200 flex justify-end space-x-4">
                    <button 
                      disabled={!selectedPptId}
                      onClick={() => setIsVideoModalOpen(true)}
                      className="px-8 py-2.5 bg-white text-indigo-700 border border-indigo-200 font-bold rounded-xl disabled:opacity-50 disabled:bg-slate-50 disabled:border-slate-200 disabled:text-slate-400 transition-all hover:bg-indigo-50 hover:shadow-sm"
                    >
                      先学习
                    </button>
                    <button 
                      disabled={!selectedPptId}
                      onClick={handleDirectExam}
                      className="px-8 py-2.5 bg-blue-600 text-white font-bold rounded-xl disabled:opacity-50 transition-all hover:bg-blue-700 shadow-md shadow-blue-100 flex items-center space-x-2"
                    >
                      <span>直接考试</span>
                      <Play className="w-4 h-4 fill-current" />
                    </button>
                  </div>
                </div>
              )}

              {/* STATE 5: PPT PRESENTING */}
              {simState === 'ppt_presenting' && (
                <div className="bg-white rounded-2xl shadow-sm border border-slate-200 flex-1 flex flex-col overflow-hidden h-full">
                  <div className="p-4 border-b border-slate-100 bg-slate-50/50 flex items-center justify-between">
                    <div className="flex items-center space-x-3">
                      <span className="text-xs font-bold bg-amber-100 text-amber-800 px-2.5 py-1 rounded-md">环节2讲解中: PPT产品演示考核</span>
                      <span className="text-slate-300">|</span>
                      <span className="text-xs text-slate-500 font-semibold truncate max-w-sm">课件：{selectedPPT?.name}</span>
                    </div>
                    <div className="flex items-center space-x-6">
                      <div className="text-xs text-slate-400">
                        课件进度: <span className="font-bold text-slate-800">{currentSlideIndex + 1}</span> / {selectedPPT?.slides.length} 页
                      </div>
                      <button 
                        onClick={handleEarlyClosePpt}
                        className="text-xs bg-white hover:bg-red-50 text-slate-600 hover:text-red-600 px-3 py-1.5 rounded border border-slate-200 hover:border-red-200 font-bold transition-all shadow-sm flex items-center space-x-1"
                      >
                        <X className="w-3.5 h-3.5" />
                        <span>中途关闭宣讲</span>
                      </button>
                    </div>
                  </div>

                  <div className="flex-1 grid grid-cols-1 lg:grid-cols-12 gap-4 p-4 bg-slate-100/50 overflow-hidden">
                    <div className="lg:col-span-7 bg-white rounded-xl border border-slate-200 shadow-sm flex flex-col overflow-hidden h-full">
                      <div className="p-3 bg-slate-800 text-slate-200 text-xs flex justify-between items-center">
                        <span className="font-bold">PPT 投影屏幕大窗</span>
                        <span className="opacity-75">16:9 比例输出</span>
                      </div>
                      <div className="flex-1 bg-gradient-to-tr from-slate-900 to-slate-800 text-white p-8 flex flex-col justify-between relative overflow-hidden">
                        <div className="absolute right-0 bottom-0 text-white/5 font-bold text-9xl pointer-events-none select-none">DIGITAL</div>
                        <div className="flex justify-between items-center border-b border-white/10 pb-4">
                          <div className="flex items-center space-x-2">
                            <div className="w-5 h-5 bg-blue-500 rounded flex items-center justify-center text-[10px] font-bold">{currentSlideIndex + 1}</div>
                            <span className="text-xs tracking-wider uppercase text-blue-400">制造数字化门户建设</span>
                          </div>
                        </div>
                        <div className="my-auto py-4 space-y-4">
                          <h2 className="text-xl font-bold text-white tracking-wide border-l-4 border-blue-500 pl-3">{selectedPPT?.slides[currentSlideIndex].title}</h2>
                          <p className="text-xs text-slate-300 leading-relaxed whitespace-pre-line bg-white/5 p-4 rounded-lg border border-white/5">{selectedPPT?.slides[currentSlideIndex].content}</p>
                        </div>
                        <div className="flex justify-between items-center text-[10px] opacity-60 border-t border-white/10 pt-4">
                          <span>数字客商在线矩阵宣讲</span>
                          <span>PAGE: {currentSlideIndex + 1} of {selectedPPT?.slides.length}</span>
                        </div>
                      </div>
                      <div className="p-2.5 bg-slate-50 border-t border-slate-200 flex space-x-2 overflow-x-auto h-20">
                        {selectedPPT?.slides.map((slide, idx) => (
                          <button 
                            key={slide.page}
                            onClick={() => setCurrentSlideIndex(idx)}
                            className={`flex-shrink-0 w-24 py-1.5 px-2 rounded border text-left text-[10px] transition-all ${currentSlideIndex === idx ? 'bg-blue-50 border-blue-500 text-blue-700 font-bold' : 'bg-white border-slate-200 text-slate-500 hover:bg-slate-100'}`}
                          >
                            <span className="block opacity-60">第 {slide.page} 页</span>
                            <span className="block truncate font-medium">{slide.title.substring(4)}</span>
                          </button>
                        ))}
                      </div>
                    </div>

                    <div className="lg:col-span-5 flex flex-col space-y-4 h-full overflow-hidden">
                      <div className="bg-white rounded-xl border border-slate-200 shadow-sm p-4 flex flex-col">
                        <div className="flex justify-between items-center mb-2">
                          <span className="text-xs font-bold text-slate-700 flex items-center space-x-1">
                            <span className="w-2.5 h-2.5 rounded-full bg-red-600 animate-pulse"></span>
                            <span>你的人像监控 (音视频正在评测中)</span>
                          </span>
                          <span className="text-[10px] bg-slate-100 text-slate-500 px-1.5 py-0.5 rounded">网络：良好</span>
                        </div>
                        <div className="aspect-video bg-slate-950 rounded-lg relative overflow-hidden group">
                          <div className="absolute inset-0 bg-cover bg-center opacity-45" style={{ backgroundImage: "url('https://images.unsplash.com/photo-1573496359142-b8d87734a5a2?auto=format&fit=crop&q=80&w=600')" }}></div>
                          <div className="absolute inset-0 bg-slate-950/40 flex items-center justify-center">
                            <div className="text-center text-white p-4">
                              <Video className="w-8 h-8 mx-auto mb-2 text-blue-400 animate-pulse" />
                              <p className="text-xs font-bold">苏晓莹 的音视频采集大窗</p>
                            </div>
                          </div>
                        </div>
                      </div>

                      {/* Recording Controls */}
                      <div className="bg-white rounded-xl border border-slate-200 shadow-sm p-5 flex flex-col items-center space-y-4">
                        {/* Microphone with water ripple */}
                        <div className="relative flex items-center justify-center w-20 h-20">
                          {isRecording && (
                            <>
                              <span className="absolute inset-0 rounded-full bg-blue-400/20 animate-ping" style={{ animationDuration: '1.5s' }}></span>
                              <span className="absolute inset-2 rounded-full bg-blue-400/30 animate-ping" style={{ animationDuration: '1s', animationDelay: '0.3s' }}></span>
                              <span className="absolute inset-4 rounded-full bg-blue-400/40 animate-ping" style={{ animationDuration: '0.8s', animationDelay: '0.6s' }}></span>
                            </>
                          )}
                          <div className={`w-14 h-14 rounded-full flex items-center justify-center z-10 transition-all ${isRecording ? 'bg-blue-600 text-white shadow-lg shadow-blue-200' : 'bg-slate-100 text-slate-500'}`}>
                            <Mic className={`w-6 h-6 ${isRecording ? 'animate-pulse' : ''}`} />
                          </div>
                        </div>

                        <div className="flex space-x-3 w-full">
                          <button
                            onClick={() => setIsRecording(true)}
                            disabled={isRecording}
                            className={`flex-1 py-2.5 px-4 rounded-xl font-bold text-sm transition-all ${
                              isRecording
                                ? 'bg-slate-100 text-slate-400 cursor-not-allowed'
                                : 'bg-blue-600 hover:bg-blue-700 text-white shadow-md shadow-blue-100'
                            }`}
                          >
                            开始录音
                          </button>
                          <button
                            onClick={() => {
                              setIsRecording(false);
                              handleNextSlide();
                            }}
                            disabled={!isRecording}
                            className={`flex-1 py-2.5 px-4 rounded-xl font-bold text-sm transition-all ${
                              !isRecording
                                ? 'bg-slate-100 text-slate-400 cursor-not-allowed'
                                : 'bg-red-500 hover:bg-red-600 text-white shadow-md shadow-red-100'
                            }`}
                          >
                            结束录音
                          </button>
                        </div>
                      </div>

                      <p className="text-center text-[11px] text-slate-400 leading-relaxed">
                        点击「结束录音」自动提交本页的内容，并翻页到下一张
                      </p>
                    </div>
                  </div>
                </div>
              )}

              {/* STATE 6: TRANSITION TO QA */}
              {simState === 'transition_to_qa' && (
                <div className="bg-slate-900 rounded-3xl shadow-xl flex-1 flex flex-col items-center justify-center p-12 text-white">
                  <div className="text-center max-w-xl space-y-6">
                    <div className="w-20 h-20 bg-indigo-600 rounded-full flex items-center justify-center mx-auto shadow-lg shadow-indigo-500/30 animate-pulse">
                      <MessageSquare className="w-10 h-10 text-white" />
                    </div>
                    <div className="space-y-2">
                      <span className="text-xs text-indigo-400 font-bold uppercase tracking-widest">王经理正在进行追问过渡...</span>
                      <h3 className="text-xl font-bold tracking-tight">
                        “{pptFinishStatus === 'early' ? '好吧，听了你的ppt我还是有很多疑惑。' : '感谢你的介绍，我已经差不多了解了，还有一些问题想和你确认。'}”
                      </h3>
                    </div>
                    <div className="flex justify-center space-x-1.5">
                      <span className="w-2 h-2 bg-indigo-400 rounded-full animate-bounce"></span>
                      <span className="w-2 h-2 bg-indigo-400 rounded-full animate-bounce delay-100"></span>
                      <span className="w-2 h-2 bg-indigo-400 rounded-full animate-bounce delay-200"></span>
                    </div>
                    <p className="text-xs text-slate-400 leading-relaxed pt-4 border-t border-slate-800">
                      PPT宣讲阶段结束。接下来，系统将无缝续接问题 {hasMaterialStage ? currentQaIndex + 3 : currentQaIndex + 2}。
                    </p>
                  </div>
                </div>
              )}

              {/* STATE 7: STANDARD QA SESSION */}
              {simState === 'qa' && (
                <div className="bg-white rounded-2xl shadow-sm border border-slate-200 flex-1 flex flex-col overflow-hidden h-full">
                  <div className="bg-white border-b border-slate-100 px-6 py-3 flex items-center justify-between">
                    <div className="flex items-center space-x-2 text-xs font-semibold text-slate-600">
                      <span className="text-slate-400">实战测评 · 制造业 · 数字门户 · 专业型客户</span>
                    </div>
                    <div className="flex items-center space-x-4">{renderSessionProgressHeader()}</div>
                  </div>
                  <div className="flex-1 grid grid-cols-1 lg:grid-cols-12 gap-5 p-5 bg-[#F8FAFC]">
                    <div className="lg:col-span-4 bg-white rounded-2xl border border-slate-200/80 shadow-sm p-4 flex flex-col justify-between">
                      <div className="flex-1 flex items-center justify-center py-4"><AnimeAvatar /></div>
                      <div className="bg-[#FAFBFD] p-4 rounded-2xl border border-blue-100 relative shadow-sm">
                        <div className="absolute -top-2 left-1/2 transform -translate-x-1/2 w-4 h-4 bg-[#FAFBFD] rotate-45 border-t border-l border-blue-100"></div>
                        <div className="flex items-center justify-between mb-2">
                          <span className="text-[10px] bg-green-100 text-green-700 font-bold px-2 py-0.5 rounded-full flex items-center space-x-1">
                            <span className="w-1.5 h-1.5 bg-green-500 rounded-full animate-pulse"></span>
                            <span>{currentQaIndex >= 1 ? '提问中' : '正在录音'}</span>
                          </span>
                          <span className="text-[10px] text-blue-600 bg-blue-50 px-2 py-0.5 rounded font-bold">{currentQuestion?.tag}</span>
                        </div>
                        <p className="text-xs text-slate-700 leading-relaxed font-medium">{questionDisplayText}</p>
                      </div>
                    </div>
                    <div className="lg:col-span-4 flex flex-col justify-between bg-white rounded-2xl border border-slate-200/80 shadow-sm p-5">
                      <div>
                        <div className="aspect-square bg-slate-950 rounded-2xl relative overflow-hidden shadow-inner border border-slate-900 flex items-center justify-center">
                          <div className="absolute inset-0 bg-[url('https://images.unsplash.com/photo-1502082553048-f009c37129b9?auto=format&fit=crop&q=80&w=600')] bg-cover bg-center opacity-60"></div>
                          <div className="absolute top-3 right-3 bg-blue-600 text-white text-[10px] font-bold px-2 py-0.5 rounded-md flex items-center space-x-1 shadow-sm">
                            <span className="w-1.5 h-1.5 bg-white rounded-full animate-ping"></span>
                            <span>REC</span>
                          </div>
                          <div className="absolute bottom-3 left-3 bg-black/50 text-white text-[9px] px-2 py-0.5 rounded">麦克风：内置通道 3</div>
                        </div>
                      </div>
                      <div className="my-4 text-center">
                        <div className="inline-block bg-slate-50 border border-slate-100 rounded-2xl px-6 py-2 shadow-sm">
                          <div className="flex items-center justify-center space-x-1.5 text-slate-400">
                            <Clock className="w-3.5 h-3.5 text-blue-500" />
                            <span className="text-[10px] font-bold tracking-wider">剩余时间</span>
                          </div>
                          <span className="text-2xl font-black text-blue-600 tracking-tight block mt-0.5">{currentQaIndex === 1 ? '05:00' : '03:22'}</span>
                        </div>
                      </div>
                      <div className="space-y-4">
                        <button onClick={handleFinishQa} className="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-3.5 px-6 rounded-2xl transition-all shadow-md shadow-blue-100 tracking-wider text-sm text-center block">
                          结束回答
                        </button>
                        <div className="grid grid-cols-3 gap-2">
                          <button className="flex flex-col items-center justify-center py-2 bg-slate-50 hover:bg-slate-100 border border-slate-200/50 rounded-xl transition-all text-slate-600">
                            <Sparkles className="w-4 h-4 text-amber-500 mb-1" />
                            <span className="text-[10px] font-bold">战术锦囊</span>
                          </button>
                          <button className="flex flex-col items-center justify-center py-2 bg-slate-50 hover:bg-slate-100 border border-slate-200/50 rounded-xl transition-all text-slate-600">
                            <RotateCcw className="w-4 h-4 text-blue-500 mb-1" />
                            <span className="text-[10px] font-bold">重新回答</span>
                          </button>
                          <button onClick={handleFinishQa} className="flex flex-col items-center justify-center py-2 bg-slate-50 hover:bg-slate-100 border border-slate-200/50 rounded-xl transition-all text-slate-600">
                            <ChevronRight className="w-4 h-4 text-slate-500 mb-1" />
                            <span className="text-[10px] font-bold">跳过此题</span>
                          </button>
                        </div>
                      </div>
                    </div>
                    {renderSessionHistory()}
                  </div>
                </div>
              )}

            </div>
          )}

          {/* ======================= TAB: RESULTS ======================= */}
          {activeTab === 'result' && (
            <div className="fixed inset-0 z-[55] bg-slate-900/60 backdrop-blur-sm flex items-center justify-center p-4 md:p-6 animate-fade-in" onClick={() => { setActiveTab('simulate'); setSimState('entry'); }}>
              <div className="bg-slate-50 w-full max-w-5xl h-[92vh] rounded-[32px] shadow-2xl flex flex-col overflow-hidden border border-white/60" onClick={(e) => e.stopPropagation()}>
                <div className="bg-white px-6 md:px-8 py-5 flex items-center justify-between border-b border-slate-100 shrink-0">
                  <h2 className="text-xl md:text-2xl font-bold text-slate-800">实战对战深度复盘报告</h2>
                  <div className="flex items-center gap-3">
                    <button onClick={() => { setSimState('entry'); setActiveTab('simulate'); }} className="px-5 py-2 bg-blue-600 hover:bg-blue-700 text-white text-sm font-semibold rounded-full shadow-sm shadow-blue-100 transition">重新测评</button>
                    <button onClick={() => { setActiveTab('simulate'); setSimState('entry'); }} className="w-10 h-10 flex items-center justify-center rounded-full bg-slate-100 hover:bg-slate-200 text-slate-500 hover:text-slate-700 transition">
                      <X className="w-5 h-5" />
                    </button>
                  </div>
                </div>
                <div className="flex-1 overflow-y-auto p-6 md:p-8">
                  <ResultPanel selectedPPT={selectedPPT} userPptAnswers={userPptAnswers} qaQuestions={qaQuestions} pptReviewSlideIndex={pptReviewSlideIndex} setPptReviewSlideIndex={setPptReviewSlideIndex} isDetailOpen={isDetailOpen} setIsDetailOpen={setIsDetailOpen} setSimState={setSimState} setActiveTab={setActiveTab} />
                </div>
              </div>
            </div>
          )}

          {/* ======================= TAB: HISTORY ======================= */}
          {activeTab === 'history' && (
            <div className="max-w-7xl mx-auto space-y-6">
              <div className="bg-white rounded-2xl shadow-sm border border-slate-200 p-6">
                <h2 className="text-lg font-bold text-slate-800">实战的历史记录</h2>
                <p className="text-xs text-slate-400 mt-1">这里展示您已完成的课程测评记录，课程标题按行业、产品类型、客户类型拼接展示，方便快速回看。</p>
              </div>
              <div className="bg-white rounded-2xl shadow-sm border border-slate-200 overflow-hidden">
                <div className="p-4 bg-slate-50 border-b border-slate-100 flex justify-between items-center">
                  <span className="text-xs font-bold text-slate-500">历史记录列表</span>
                  <span className="text-xs text-slate-400">共计 {historyList.length} 条记录</span>
                </div>
                <div className="overflow-x-auto">
                  <table className="w-full text-left text-xs">
                    <thead className="bg-slate-50 border-b border-slate-100 text-slate-400 font-semibold uppercase">
                      <tr>
                        <th className="p-4">行业 / 产品类型 / 客户类型 / 回合</th>
                        <th className="p-4">关联讲授 PPT 课件名称</th>
                        <th className="p-4">对战日期</th>
                        <th className="p-4">实战表现</th>
                        <th className="p-4 text-center">操作</th>
                      </tr>
                    </thead>
                    <tbody className="divide-y divide-slate-100 text-slate-600">
                      {historyList.map((record) => (
                        <tr key={record.id} className="hover:bg-slate-50/50 transition-all">
                          <td className="p-4">
                            <div className="font-bold text-slate-800">{record.path}</div>
                            <div className="text-[10px] text-slate-400 mt-0.5">第 {record.id} 回合</div>
                          </td>
                          <td className="p-4">
                            <div className="flex items-center space-x-2 text-slate-700 font-medium">
                              <FileText className="w-4 h-4 text-slate-400 flex-shrink-0" />
                              <span className="truncate max-w-[220px]" title={record.pptName}>{record.pptName}</span>
                            </div>
                          </td>
                          <td className="p-4 text-slate-500">{record.date}</td>
                          <td className="p-4">
                            <span className={`inline-block font-bold px-2.5 py-1 rounded-full text-[10px] ${record.score === '0分' ? 'bg-red-50 text-red-600' : record.score.startsWith('1') || record.score.startsWith('2') ? 'bg-amber-50 text-amber-600' : 'bg-blue-50 text-blue-600'}`}>
                              {record.score}
                            </span>
                          </td>
                          <td className="p-4">
                            <div className="flex justify-center space-x-2">
                              <button onClick={() => setActiveTab('result')} className="bg-slate-100 hover:bg-slate-200 text-slate-700 px-3 py-1.5 rounded-lg font-bold transition-all">查看结果</button>
                              <button onClick={() => { setSimState('entry'); setActiveTab('simulate'); }} className="bg-blue-50 hover:bg-blue-100 text-blue-600 px-3 py-1.5 rounded-lg font-bold transition-all">重新测评</button>
                            </div>
                          </td>
                        </tr>
                      ))}
                    </tbody>
                  </table>
                </div>
                <div className="p-4 border-t border-slate-100 bg-slate-50/50 flex justify-between items-center text-xs">
                  <span className="text-slate-400">显示第 1-{Math.min(4, historyList.length)} 条，共 {historyList.length} 条</span>
                  <div className="flex space-x-1">
                    <button className="px-2.5 py-1 rounded border border-slate-200 bg-white text-slate-400" disabled>上一页</button>
                    <button className="px-2.5 py-1 rounded border border-blue-500 bg-blue-50 text-blue-600 font-bold">1</button>
                    <button className="px-2.5 py-1 rounded border border-slate-200 bg-white hover:bg-slate-50 text-slate-600">下一页</button>
                  </div>
                </div>
              </div>
            </div>
          )}

        </div>
      </div>
    </div>
  );
}
